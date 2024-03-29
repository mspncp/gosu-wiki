# Ruby Chipmunk Integration

A tutorial contributed by Dirk Johnson. This wiki page explains in prose how to extend the [[Ruby Tutorial]] with the Chipmunk Physics Engine. The result is [this Ruby code](https://github.com/gosu/gosu-examples/blob/master/examples/chipmunk_integration.rb) in the `gosu-examples` gem. Install both the `chipmunk` and `gosu-examples` gems, then run `gosu-examples` to see physics engine in action.

This tutorial assumes that both Gosu and Chipmunk have been properly installed.  See http://wiki.slembcke.net/main/published/Chipmunk. The source code for this tutorial can be found in Gosu's 'examples' folder, but to run it, you'll need to copy the chipmunk extension there too if you haven't installed it system-wide.

New, better documented bindings to Chipmunk 5.3.4 are available at [[http://github.com/beoran/chipmunk]]. Check there too for the documentation. --Beoran.

There are a few more examples in this [GitHub repository by PhilCK](https://github.com/PhilCK/Chipmunk-Examples).

## Prolog

Lately, I have been writing a game I have been threatening to write on-and-off for a long time.  I am, of course, using Ruby as the implementation language and Gosu as the animation layer.  One thing I faced early on was implementing the physics of the game; following one of my coding mantras, I took the approach of "get it to work first, worry about optimizing later". While the performance I saw was basically adequate for the scope of version 0.1, I could see it would start to bog down fairly quickly going forward.  As it happens, I showed Julian an early copy of my work and he pointed me to Chipmunk to handle the physics.

Can I just say, Chipmunk is awesome: it is awesome because it is fast and it is simple to use.  And it is *really* awesome because, like Gosu, it supports both Mac OS X and Ruby!  Not to put too fine a point on it, in its current iteration (as of this writing, version 3), Chipmunk is a 2D, Euler space, rigid body, physics engine.  This is quite a mouthful, and, for the most part, all y'all need worry about is "2D" which means it will mesh quite well with Gosu.

After looking at the Chipmunk framework, one thing I noticed was that it basically assumes that you are working with a profile oriented environment where down (the direction of gravity) is towards the bottom of the screen.  What this means is that you can exploit all Chipmunk offers (e.g., gravity, friction, collision detection, etc.) for your side-scrolling games, however, top-down games, where down is out the back of the display, might limit what Chipmunk can do for you, or, at least, render it more difficult to use.

Of course, my game is top-down.

So, that left me with discovering just what Chipmunk v3 could do for me.  I could have started the discovery process by ripping apart my code and attempting to integrate Chipmunk back in, but I decided to take a much simpler first step... take the top-down Tutorial for Gosu and integrate Chipmunk into that.  I even thought I would do it one better and document the conversion as a sort-of tutorial; thus what you are reading now.

Let us begin...

## Chipmunk 101

### Universal Attributes

Lets look at the Tutorial's Player class.  Notice it has instance variables for tracking what I call the universal attributes of a game object:

  * @x - The horizontal position of the Player
  * @y - The vertical position of the Player
  * @vel_x - The velocity of the x attribute of the Player
  * @vel_y - The velocity of the y attribute of the Player
  * @angle - The angle or facing of the Player

With Chipmunk, your game objects will no longer track your universal attributes, instead, your game objects will have a Chipmunk Body (sometimes called a rigid body) instance (CP::Body), which will track your universal attributes for you.  This is a good thing.  Now your game objects can focus on what makes them unique.

### Space To Play

In the Tutorial, collision analysis was done by the Player object, however, when you really think about it, determining whether one object collides with another object is really the purview of the universe in which your game objects live.  Luckily, Chipmunk provides us a "universe" object called Space (CP::Space).  Space is responsible for defining gravity and damping as well as keeping track of the Bodies and Shapes that exist within.  (Note: you can have none, one, or many Spaces in your game, easily allowing variable forces on your game objects, however, this tutorial assumes one Space.)

### Shapely Objects

The astute student will have noticed I snuck in a new term in the last paragraph: Shape.  While the Body is used to track universal attributes, the Shape (CP::Shape) is used to define the physical boundaries of those attributes.  Since a Shape is defined as being physical, it is primarily used for collision detection.  As one might guess, a Shape is pretty useless without a Body, therefore, each Shape has a Body.  This means that our game objects need only have a single reference to a Shape and they automatically get a Body, too!  It should be noted that your Shapes need to be convex shapes, which means all internal angles are less than or equal to 180 degrees.  Visually, this means no dimples in the shape.  If the game object being defined is more complex than a single convex shape can define, then a game object can have more than one Shape, that, when pieced together, form the overall shape of the object.  In this case, each Shape should point to the same Body.  (To me it is a bit awkward to have the Shape own the Body, considering that a game object could have more than one Shape but only need a single Body - rather, I would have the Body own the Shape(s).  This is, however, a minor detail and easily worked around.)

### Oh! Did That Connect?

In order to detect "collisions", the Tutorial cycled through every Star every update and judged the distance between the Player and the Stars; if the distance was less than a threshold (in this case, 35), then there was a collision and the Star was removed and the score increased by 10.  Now that game objects have Shapes, we can let Space do this work for us.  One might ask, "How do we tell Space to increment the score and remove the Star when there is a collision?"  I'm glad you asked, and the answer is "Ruby blocks!"  Space allows us to define blocks of code (sometimes called closures) that will be called when a Player collides with a Star (or, more generically, when one collision type collides with another collision type).  This allows us to increment the score and remove the Star from Space automagically!  Pretty cool.

### Beginning With The End In Mind

Go ahead and run the ChipmunkIntegration.rb; it is located at the end of this tutorial.  The ship (Player) performs like I like the ship to perform.  You may prefer a different feel.  Notice I added a "reverse" (the down button).  When you are through getting a feel for where we are heading, lets get our hands dirty.

(Note: The code at the end of this tutorial is commented and explains things this tutorial does not mention so be sure to read the comments in the code as well.)

## Getting Our Hands Dirty

### Send In The Player

Now that we understand the Chipmunk concepts that we need to apply to our game model, lets update the Player class by removing the following:

  * Remove the score - it will be tracked by the game environment (Gosu::Window) so that Space has access to it
  * Remove the beep - it will be sounded by the game environment (Gosu::Window) so that Space has access to it
  * Remove the universal attributes - they belong to the Body
  * Remove the move method - Chipmunk will do that for us
  * Remove the collect_stars method - Space will handle this for us

Now that we have ripped out the undesirable characteristics of our Player, lets rebuild it in our new, Chipmunkified image.  Following along in the code may help:

  * Add an attr_reader for :shape
  * Add a Shape parameter to your initialize method
  * Add a @shape instance variable to track the Shape
  * Initialize the Shape's position, velocity, and angle
  * Update warp to set the position in the Body
	  * Note that position is a CP::Vec2 vector
  * Update turn_left to apply torque to the Body
	  * I will explain the SUBSTEPS constant when we cover stepping Space
  * Update turn_right to apply torque to the Body
  * Update accelerate to apply force to the Body
          * Since force is a vector and we need to apply it in the direction of the angle I have added a method on the Numeric class to turn a radian scalar into a vector. See the code at the end of this document for more information
  * Add the boost method and apply force to the Body
  * Add the reverse method and apply force to the Body
  * Update the draw method to use the Body angle, but be sure to convert from radians to degrees
	  * One thing to note is that Gosu has 0 degrees (0 radians) starting at the top of the screen and Chipmunk has 0 radians (0 degrees) pointing to the right. This is handled in our Numeric#radians_to_gosu method)

### Stars In Your Eyes

Lets next update the Star class.  This is actually quite trivial:

  * Remove the attr_reader for :x and :y
  * Remove the @x and @y instance variables; I bet by now, you can tell me why
  * Add an attr_reader for :shape
  * Add a Shape parameter to your initialize method
  * Add a @shape instance variable to track the Shape
  * Initialize the Shape's position, velocity, and angle
  * Update the draw method to use the Body angle converted to degrees

See, that wasn't so bad, was it?  And, we are half way there!

### Setting Up The Environment

Initializing the environment properly is key to the whole physics engine working well.  Lets take this one step at a time by starting from scratch.  Referring to the code at the end of this tutorial will make things a lot clearer as you read:

  * First of all, add the @beep and @score that was previously part of the Player to the Gosu::Window and initialize method.  
  * Create an instance variable called @dt and set it to 1.0/60.0.
	  * This variable specifies how long a step represents in Space
  * Assign an instance variable called @space a new CP::Space
  * Initialize @space.damping to 0.8
	  * 1.0 is no damping and 0.0 is full damping
	  * I think of damping as being similar to an ambient friction in Space
  * Create the Body for the player and assign it a mass of 10.0 and a moment of inertia of 150.0
	  * Think of the moment of inertia as an object's resistance to torque
  * Lets use a 4 vertex polygon to define the shape of the ship
	  * The "top" of the polygon should be oriented towards 0 radians (the right)
  * Create the poly Shape for the Body
  * Set the collision_type of the Shape to :ship
  * Add both the Body and the Shape to Space
  * Create an @player instance variable and instantiate a Player instance using the new Shape
  * Warp the player to the middle of the screen (320, 240)
  * As in the previous Tutorial, continue to initialize the star animation and Stars arrays

We are now ready to set up the rules for a collision between a :ship and a :star.  There is one critical thing to be aware of.  Within the block of code representing the rules for a collision, you are not allowed to modify the contents of Space.  This means you must keep track of what you want to modify and then modify away after the block of code has completed executing.  For this purpose, as we want to remove Stars from Space, we will create a @remove_shapes instance variable.

  * Create @remove_shapes and initialize it to an empty array
  * Add a collision function to Space for a collision between :ship and :star,
	  * Increase the score by 10
	  * Beep
	  * Add the Star's Shape to the @remove_shapes array
	  * Note that a collision closure receives references to both colliding shapes 

What may not be obvious is that for things to work properly in our game, we need to define a second collision block in the case of one :star hitting :another.  You might ask how this could happen.  I'm glad you asked.  The way it could happen is that between the time that a :ship collides with a :star and the time the Star is removed from Space, the Star travels and may collide with another Star, thus moving that Star.  Since our Stars are intended to be stationary, we need to tell Space to ignore collisions between two :stars.  We do this by passing a nil block (&nil).

  * Add a collision function to Space for a collision between :star and :star
	  * Pass a nil block to instruct Space to ignore these collisions
    
Wow, we are done initializing our physics environment.  We are almost through with the conversion!  This is pretty fun, huh?  Onward.

The next step is to integrate stepping Space with the Gosu::Window update.  One thing to note about the Chipmunk engine is you can lose collisions, meaning Shapes that should have been reported as a collide can go unreported when one or both of those Shapes have a large momentum.  The reason is that between steps the Shapes can travel so far as to pass each-other.  The trick, then, is to step Space with a small enough increment that you make such a miss highly unlikely.  In the Tutorial below, I have added a SUBSTEPS constant which lists how many times Space should be stepped per Gosu::Window update.  This may be adjusted as needed.  I personally like the feel of the game when SUBSTEPS is 6.  In the Gosu::Window update method, do the following:

  * Create a loop using SUBSTEPS and do the following within this loop:
	  * Cycle over the @remove_shapes array and
		  * Delete the Star from the @stars array that corresponds to the current shape
		  * Remove the Shape's Body from Space
		  * Remove the Shape from Space
	  * Clear the @remove_shapes array
	  * Reset the forces on the Player's Body
		  * As force and torque added to a body are cumulative, they should be reset every step
	  * Tell the Player to validate its position on the screen
	  * Check the keyboard for inputs
		  * Don't forget to check for boost and reverse
	  * Step Space using @dt as the time value
  * Outside the loop, continue to add stars as in the old Tutorial		

Congratulations!  You have converted the Gosu Tutorial to using Chipmunk!  And, along the way, you should have been armed with most of what you need to do the same to your games.  I hope you enjoyed this as much as I did, and I hope you make some awesome stuff with Gosu and Chipmunk (ChipSu?).

### Epilog

As of this writing, Chipmunk's Ruby bindings documentation is out of date.  On the Chipmunk forums, the author, Scott Lembcke, has said he will be updating the docs and will "soon" release version 4.  In the meantime, scour the C documentation, the code, and the forums.  I will do my best to update this tutorial for version 4 when it is released.
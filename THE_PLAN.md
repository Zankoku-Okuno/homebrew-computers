The thing that seems to be working for me right now is the svg visualizer.
I think I should focus on that and worry about the other stuff later.
Further, I am designing for breadboards right now, and should focus on that use case.
Other design formats can come later.

In particular, the layers are:
    * reference coordinates
    * conductiong strips
    * socket
    * components
    * insulated wires
    * silkscreen?

I'm going to use Haskell as the scripting language.
The API I need to expose to the user's scripts ends up being essentially an svg element appender.
Actually, haskell-plugin is quite slow; it's probably better to not use it, unfortunately.

Since connectivity is given by geometry in the real world, it should be derivable from the geometry of the svg sketch.
Simulation of the circuit would require each component to give an implementation of its internals.


If I want to do drwaing relative to a module, at the moment I have to manually add in the module offsets.
Instead of using plain ints in Haskell, I could easily wrap them in a newtype that can only be unwrapped into a reader monad.


Oh, also: There are a bunch of wires with offsets, and then the mirror image on the other side of the midline.
Calculate the column off the midline with an offset that is pos/neg for each side.
The actual groups of wires are little more than a bunch of identical straight lines just on different rows.
##Authors Note##
This is somewhat out of date, and in any case was concieved from a faulty premise; I think there's potential value in having a legible syntactic construct for defining and organizing rule systems, but inheritance as a foundational principle complicates things in a lot of counter-intuitive ways, destroying the ideal of expressive elegance that I hope for. I need to think of someting else, but this really takes a back seat to more pressing (i.e. paying) projects. I'm open to suggestions though, so if you have an idea, shoot me an email or submit a pr or something and we'll see what's what.

#Ur#

A language convention for defining games and game systems using inheritance and other concepts from programming.

Any game is, at its core, a system of rules. I strive therefore to build a universal system for describing rules that is concise, powerful, and easy to use. It makes use of Inheritance and looks like this:

Rule(Parent 1, ... , Parent n)
{What refines this rule from its parents.}

"Rule" is assumed to be the parent category (or type) for everything. Every part of a game system is a rule. But by using inheritance, we can declare generalizations:

Object(Rule)
{Objects are things that exist within the game world.}

Tool(Rule)
{Tools are things that exist in the real world and are used by the game.}

Action(Rule)
{Actions are things Objects do in the game world. Action names should generally be verbs for easy in-line reference.}

So that, say, in chess, Pawn(Object) and Pawn(Tool) mean two different things. But there's no reason a given rule must inherit from only one parent:

Piece(Tool)
{Pieces are what the players move around the board in order to enact the game. Each piece can move any distance (in squares) in any direction. No piece may change direction during a movement, and only one piece may move per turn.}

Taking(Action)
{The act of one piece moving into a square occupied by an enemy piece. The enemy piece is taken by the active player, removed from the board, and may no longer act in this game.}

Pawn(Piece, Object)
{Moves 1 Square forward [or however this direction is defined in Chess] except when Taking.
When Taking, moves 1 Square diagonally, forward and either left or right.
Becomes a Queen upon reaching the Enemy border.}

A Parent rule is assumed to be true unless stated otherwise for a given child, so the only rules that are absolute are those of children that are not also parents.

The hope, therefore, is that by making good use of inheritance, we can make it faster and easier for a designer to describe a given system in all necessary detail; you only have to state a given rule once, and it is assumed for all its children, except where those children explicitly state otherwise. Writing explicit definitions in this way may also help to clarify the system in the mind of the designer, and it makes it easier to condense and index the rules for speedy reference during a game.

Something else Ur tries to make use of is Libraries. Libraries are packaged sets of related rules and systems that a designer can import into his or her designs without having to rewrite all of those rules. Anyone can write their own Library (in a sense, that's what any game written in Ur is doing) and I believe that the real power of Ur will come from Libraries. The end goal is that a designer doesn't even have to print or package a public library with his or her game, but can just say something like "This game depends on x" and then ship only the rules that are specific to the game in question. (Like inheritance, this is a tool for formalizing generalizations). Ideally, a given Library strikes the right balance between usefulness and specificity. The best Library is one of which most of its users use most of the definitions it provides. This makes it easier for users new to Ur to find only what they need for their game, instead of having to sift through one gigantic library of everything the community could possibly think of. To begin with, Ur ought to have a few core Libraries, rules that make the biggest possible generalizations about games and how games work. From there, it makes sense to start branching off, to build libraries for different subsets of gaming communities. Tabletop RPG designers (and players), for example, will generally use rules for character generation, world-building, and conflict arbitration, while designers of more abstract games (like Hive, or Chess) will use none of those things, but will probably use libraries describing pieces and board movement.

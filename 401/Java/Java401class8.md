# Object Oriented Design

## Don't Repeat Yourself (DRY)

- DRY is a principle of software development aimed at reducing repetition of software patterns, replacing it with abstractions or using data normalization to avoid redundancy.
- when DRY principle is applied successfully, a modification of any single elemtn of a system does not require a change in other logically unrelated elements.
- elements that are logically related all change predictably and uniformally, and thus are kept in sync.

## WET

- WET is the oppositve of DRY and stands for "write everything twice".
- WET solutions are common in mult-tiered achitectures where a developer may be tasked with, for example, adding a comment field on a form in a web application.

## AHA

- AHA stands for "avoid hasty abstractions".
- optimize for change first, and avoid premature optimization.
- AHA assumes that both WET and DRY solutions inevitably create software that is too rigid and difficult to maintain.
- software can me more flexible and robust if abstraction is only done when it is needed.

## You aren't gonna need it (YAGNI)

- YAGNI is a principle that states a programmer should not add functionality until deemed necessary.
- "Always implement things when you actually need them, never when you just foresee that you need them".
- YAGNI is a principle behind the XP practice of "do the simplest thing that could possibly work".
- used in combinationi with several other practices, such as continuous refactoring, automated unit testing and integration.
- used without continuous refactoring and it could lead to disorganized code and massive rework, known as technical debt.

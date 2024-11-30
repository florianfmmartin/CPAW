# CPAW machine

Contained Packages Assembled by Workers

## What

CPAW is an abstract machine inspired by SECD, Join-Calculus, and Rewriting Systems.

## Implementation

The implementation is in [this IMD notebook](./cpaw.md).

[IMD is a simple notebook format](https://github.com/florianfmmartin/imd).

## Concepts

### Packages

Packages have a name, a container to go into, and upto 3 data slots.
The first slots is the object, the second the relation, and the third the subject.
These are informal names for the slots, packages may use them as they wish.

### Containers

Containers have a name, and contain packages.

### Workers

Workers have a name, and a list of assembly recipes.
A worker's recipe are ordered and only one will be excute by turn.
So the recipes should be different patterns triggering a similar job,
not different jobs.

### Assembly recipes/Assemblers

Assembly recipes have a name, conditions, and consequences.
A condition is a pair of container and package .
A consequences is a pair of container name and package.
They have acces to a small sub-lang that has a few instructions.

## Execution

Packages are put into containers from outside the runtime, and taken from containers from outside the runtime via conventions.
Execution starts by putting the start package in the start container.
Then all workers try to work, one after the other, until halting.
When a worker tries to worker:
1. they check their first assembler for conditions
2. if all conditions are met, the assembler executes and the worker stops until he's woken up again
3. if not, then the second recipe's conditions are checked, and so on
4. if no recipe match, then the worker goes to sleep


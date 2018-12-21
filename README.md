# Polling-Algos
An exploration of different methods of resolution of Doodle Polls


Problem Formulation:
Suppose we have a supervisor, and n supervisees. Each supervision takes 1 hour, and the supervisor has m supervision slots.
Each student has a certain set of preferences for the times (i.e. some slots are perfect, and they might not be able to attend others).
In one variant, we might want to work out if any assignment of students to slots is feasible, meaning that each slot has at most one student.
An example of an infeasible preference set is whenever m < n, or when each student can only do the first slot.
Another variant is deciding how to pick the best assignment, where best is defined by some ordering which will be defined later.

Variant 1: Our input is n arrays, each of size m, representing the preferences of the students for each slot. Each array will be a permutation of the elements 1 to m, and our job is to find an assignment of each student to a slot, such that the sum of each student's preference for his assigned slot is minimized. We assume m >= n, so the problem is always feasible.

Variant 2: We use the same input data, but instead of each array being a permutation, we allow, for each student i, a number i_c, such that for each choice with preference >= i_c, we replace it with 'infinity', i.e. representing an infeasible choice. We want to (a) work out whether we can do the assignment in a feasible way, and then if so, work out the best choice again.

There is a solution to both variants together: the Hungarian algorithm, with complexity max(m, n)^3.
https://en.wikipedia.org/wiki/Hungarian_algorithm

But is there a solution to Variant 2, when we just want to work out if there is a feasible choice, and such that it beats the Hungarian algorithm's complexity?

For the solution, we translate the problem into a graph theory problem, and use Hall's theorem (Note we are ignoring the value of the preference. We have 2 sets of vertices, denoting the students, and the slots, and draw a line between a slot and a student if a student is using that slot). Then we want a 'perfect matching' in some sense. Unfortunately, a perfect matching only makes sense when m = n.
but we know m>=n, so we can add dummy students, m-n of them, each with no preference whatsoever (this doesn't change the problem at all).
Then we can apply Hall's marriage theorem.

Unfortunately, the Hall Marriage condition involves checking 2^m conditions, so there is probably not a better way than the Hungarian Algorithm. Specifically, we apply the Hungarian algorithm to the problem, and if the sum of our best assignment is infinity, there is no perfect matching; otherwise there is.




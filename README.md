# Towards Human-centric AutoML via Logic and Argumentation

This repository contains detailed instructions on how to run the examples form the the work _Towards Human-centric AutoML via Logic and Argumentation_.

## Set up the environment

In this part we will prepare the environment required to run all the examples.

1. Install the [Java runtime](https://adoptium.net/releases.html?variant=openjdk11&jvmVariant=hotspot) (version **11** or above). If Java is already present on your system, you can skip this step.
2. Download the stand-alone [Arg2P Java IDE](https://github.com/tuProlog/arg2p-kt/releases/download/0.6.1/arg2p-ide-0.6.1-redist.jar).
3. If Java is correctly installed, with a double click on the file downloaded at step 2 (__arg2p-ide-0.6.1-redist.jar__), this should be the result.
![arg2p](https://user-images.githubusercontent.com/41596745/155752310-b3d42d4b-6034-4b48-96f5-c6f1500301ff.png)
If nothing happens, check your _Java_ installation by following the instructions at point 1.
4. You are now ready to run the example!

## 

1. Pass the following theory in the _theroy_ section.

```
t1 : [] => transformation(discretization).
t2 : [] => transformation(normalization).
a1 : [] => algorithm(dt).

c1 :=> mandatory_transformation_for_algorithm([discretization], dt).
c2 :=> invalid_transformation_set([normalization, discretization]).

% The following part is the engine that allows the argumation to be performed. It will be hidden, since will be part of the HAMLET framework.

g0 : algorithm(Z) => pipeline([], Z).
g1 : transformation(X), transformation(Y), algorithm(Z), prolog(X \== Y) =>
pipeline([X, Y], Z).
g2 : transformation(X), algorithm(Z) => pipeline([X], Z).

conflict([invalid_transformation_set(X)], [pipeline(Z, _)]) :-
\+ (member(Y, X), \+ member(Y, Z)).

conflict([mandatory_transformation_for_algorithm(X, Y)], [pipeline(Z, Y)]) :-
member(T, X),
\+ member(T, Z).
```

2. To require the evalution use the predicate `buildLabelSets`. Just put it in the query section (__?-__) and press the __Solve__ button.
![hamlet](https://user-images.githubusercontent.com/41596745/155752381-b7c967c4-1019-435f-a71d-52c0231a8a63.png)


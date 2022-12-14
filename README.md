# Final Exam Preparation

The problems below are similar to what you can expect for the final
exam. Though note that:

* There are more exercises than what I expect you to be able to
  complete in 2 hours.
  
* Some of the exercises are a bit harder than what you'd see in the exam.

## Lambda Calculus

1. For each of the following lambda calculus terms, compute the set of
   free variables and show an alpha-renaming of the term such that no
   variable is bound more than once.
   
   1. *(λ x. x y) z*
      
       <details><summary>Solution</summary>
       <p>
     
       Free variables: *y, z*
       
       Renaming: *(λ x. x y) z*
     
       </p>
      </details>
   

   1. *(λ x. (λ x. x) x) (λ x. x)*
      
      <details><summary>Solution</summary>
       <p>
     
       Free variables: none
       
       Renaming: *(λ x1. (λ x2. x2) x1) (λ x3. x3)*
     
       </p>
      </details>
      
   1. *(λ x. (λ x. x) x) (λ x. x) y* 
   
      <details><summary>Solution</summary>
       <p>
     
       Free variables: *y*
       
       Renaming: *(λ x1. (λ x2. x2) x1) (λ x3. x3) y*
     
       </p>
      </details>

1. Show the reductions to normal form of the following lambda calculus
   terms, assuming the definitions provided in the class notes. Show
   each beta-reduction step.


   1. *`or` `false` `1`*

      <details><summary>Solution</summary>
      <p>
     
      *`or` `false` `1`*

      *= (λ a b. a `true` b)* `false` `1`*
     
      *->-> `false` `true` `1`*
     
      *= (λ x y. y) `true` `1`*
     
      *->-> `1`*
     
      </p>
      </details>

     
   1. *`iszero` `1` `2` `3`*
   
      <details><summary>Solution</summary>
      <p>
     
      *`iszero` `1` `2` `3`*
      
      *= (λ n. n (λ x. `false`) `true`) `1` `2` `3`*
      
      *-> (`1` (λ x. `false`) `true`) `2` `3`*
      
      *= ((λ s z. s z) (λ x. `false`) `true`) `2` `3`*
      
      *->-> ((λ x. `false`) `true`) `2` `3`*
      
      *-> `false` `2` `3`
      
      *= `(λ x y. y)` `2` `3`
      
      *->-> `3`*

      </p>
      </details>

   1. *`pred` `1`*
   
      <details><summary>Solution</summary>
      <p>
     
      *`pred` `1`*
      
      *= (λ n. `snd` (n (λ p. `pair` (`succ` (`fst` p)) (`fst` p)) (`pair` `0` `0`))) `1`*
      
      *-> `snd` (`1` (λ p. `pair` (`succ` (`fst` p)) (`fst` p)) (`pair` `0` `0`))*
      
      *= `snd` ((λ s z. s z) (λ p. `pair` (`succ` (`fst` p)) (`fst` p)) (`pair` `0` `0`))*
      
      *->-> `snd` ((λ p. `pair` (`succ` (`fst` p)) (`fst` p)) (`pair` `0` `0`))*
  
      *-> `snd` (`pair` (`succ` (`fst` (`pair` `0` `0`))) (`fst` (`pair` `0` `0`)))*
      
      *=  `snd` (`pair` (`succ` (`fst` (`pair` `0` `0`))) (`fst` ((λ x y b. b x y) `0` `0`)))*
      
      *->-> `snd` (`pair` (`succ` (`fst` (`pair` `0` `0`))) (`fst` (λ b. b `0` `0`)))*
      
      *= `snd` (`pair` (`succ` (`fst` (`pair` `0` `0`))) ((λ p. p `true`) (λ b. b `0` `0`)))*
      
      *-> `snd` (`pair` (`succ` (`fst` (`pair` `0` `0`))) ((λ b. b `0` `0`) `true`))*
      
      *-> `snd` (`pair` (`succ` (`fst` (`pair` `0` `0`))) (`true` `0` `0`))*
      
      *= `snd` (`pair` (`succ` (`fst` (`pair` `0` `0`))) ((λ x y. x) `0` `0`))*
      
      *->-> `snd` (`pair` (`succ` (`fst` (`pair` `0` `0`))) `0`)*
      
      *= (λ p. p `false`) (`pair` (`succ` (`fst` (`pair` `0` `0`))) `0`)*
      
      *-> (`pair` (`succ` (`fst` (`pair` `0` `0`))) `0`) `false`*
      
      *= ((λ x y b. b x y) (`succ` (`fst` (`pair` `0` `0`))) `0`) `false`*
      
      *->->-> `false` (`succ` (`fst` (`pair` `0` `0`))) `0`*
      
      *= (λ x y. y) (`succ` (`fst` (`pair` `0` `0`))) `0`*
      
      *->-> `0`*
      </p>
      </details>
      

1. A list can be represented in the lambda calculus by its *fold*
   function. For example, a list *xs* containing *`1`*, *`2`*, and
   *`3`* becomes a function that takes two arguments *f* and *z* and
   returns *f `1` (f `2` (f `3` z))*:

   *xs = λ f z. f `1` (f `2` (f `3` z))*

   Now, if one wants to implement, e.g., a function that sums up all
   the elements in a list *xs* containing Church numerals, this can be
   done as follows:

   *`sum` = λ xs. xs `plus` `0`*

   In particular, applying `sum` to the list *xs* defined above yields:

   *`sum` xs → ... → `plus` `1` (`plus` `2` (`plus` `3` `0`)) → ... → `6`*

   1. Write a lambda term `nil` that represents the empty list `()`.

   2. Write a lambda term `cns` that takes an element *hd* and a list
      *tl* (represented as a fold function) and returns a list formed
      by prepending *hd* on *tl*.
   
   3. Write a lambda term `isnil` that takes a list *xs* and returns
      `true` if *xs* is the empty list and `false` otherwise.
   
   4. Write a lambda term `head` that takes a non-empty list *xs* and
      returns the head of the list (i.e. the left-most element).

   5. Write a lambda term `tail` that takes a non-empty list *xs* and
      removes the remainder of *xs* obtained after removing its
      head. This is quite a bit harder and requires a trick analogous
      to the one used to define `pred` on Church numerals (see the
      class notes).


   <details><summary>Solution</summary>
   <p>I am using OCaml syntax in the sample solution so that you can run the code in the MiniML interpreter from Homework 7.
   
      ```ocaml
	  (** booleans and pairs *)
      let ttrue = fun x y -> x in
      let tfalse = fun x y -> y in
      let pair x y = fun b -> b x y in
      let fst p = p ttrue in
      let snd p = p tfalse in
	  
      (** lists *)
      let nil = fun op z -> z in
      let cns hd tl = fun op z -> op hd (tl op z) in
      let isnil xs = xs (fun x acc -> tfalse) ttrue in
      let head xs = xs (fun x acc -> x) tfalse in
      let tail xs = snd (xs (fun x p -> pair (cns x (fst p)) (fst p)) (pair nil nil)) in
	  
      (* a small test *)
      let xs = cns 1 (cns 2 (cns 3 (cns 4 nil))) in

      (tail xs) (fun x acc -> x + acc) 0
	  ```
   </p>
   </details>

## Type Inference

For each of the following OCaml functions, decide whether they are
well-typed. If yes, provide the type of the function. Otherwise,
explain the type error. You do not need to provide any typing
constraints or calculate the unifier explicitly.


1. 
   ```ocaml
   let f x y z = if x then not y else z
   ```
   
   <details><summary>Solution</summary>
     <p>Well-typed: `f: bool -> bool -> bool -> bool` </p></details>

2. 
   ```ocaml
   let g x = if x then x + 1 else x - 1
   ```
   
   <details><summary>Solution</summary>
   <p>Not well-typed. The variable `x` is used both as a condition in the
   conditional, forcing its type to be `bool`, as well as an operand of
   `+` and `-`, forcing its type to be `int`. </p></details>
 
3.
   ```ocaml
   let rec h x = if x then h x + 1 else h x - 1
   ```
   
   <details><summary>Solution</summary>
     <p>Well-typed. `h: bool -> int` </p></details>
 
4. 
   ```ocaml 
   let i f = f true + f 0
   ```
   
   <details><summary>Solution</summary>
     <p>Not well-typed. The application `f true` forces `f` to be a type of
   the form `bool -> 'a` for some `'a` and the application `f 0`
   forces it to be `int -> 'b` for some `'b`. </p></details>
 
5. 
   ```ocaml
   let j x =
     let f y = x in
     f true + f 0
   ```
   
   <details><summary>Solution</summary>
     <p>Well-typed. `j: int -> int`
      </p></details>
6. 
   ```ocaml
   let rec k = function
   | [] -> 0
   | x :: xs -> x + k xs
   ```
 
   <details><summary>Solution</summary>
     <p>Well-typed. `k: int list -> int`
     </p></details>

7. 
   ```ocaml
   let l = function
   | None -> false
   | Some x -> x + 1
   ```
 
   <details><summary>Solution</summary>
     <p>Not well-typed. The first match case returns a value of type `bool`
   and the second match case a value of type `int`. However, the two
   types must be equal. </p></details>
 
8.
   ```ocaml
   let rec m = function
   | None -> 0
   | Some x -> x
   | [] -> 0
   | x :: xs -> x + m xs
   ```
   
   <details><summary>Solution</summary>
     <p>Not well-typed. The patterns of the first two match cases match
   values of type `'a option` for some `'a` and the last two match
   cases match values of type `'b list` for some `'b`. However, all
   patterns must match values of the same type. </p></details>
   
## Type Inhabitation

Assume we are given the following algebraic data type:

```ocaml
type ('a,'b) either = 
  | Left of 'a 
  | Right of 'b
```

Write OCaml functions that satisfy the following polymorphic type
signatures:

* `f: ('a, 'a) either -> 'a`

  <details><summary>Solution</summary>
     <p>
     
     ```ocaml
     let f x = match x with
       | Left a -> a
       | Right a -> a
     ```
     </p></details>

* `g: ('a, 'b) either * ('a, 'c) either -> ('a, 'b * 'c) either`

  <details><summary>Solution</summary>
     <p>
     
     ```ocaml
     let g (x, y) = match x, y with
       | Left a, _ -> Left a
       | _, Left a -> Left a
       | Right b, Right c -> Right (b, c)
     ```
     </p></details>
     
* `h: 'a -> ('a -> 'b) -> ('a -> 'c) -> 'b * 'c`

  <details><summary>Solution</summary>
     <p>
     
     ```ocaml
     let h x y z = (y x, z x)
     ```
     </p></details>

* `i: 'a -> (('b -> 'a) -> 'c) -> 'c`

  <details><summary>Solution</summary>
     <p>
     
     ```ocaml
     let i x y = y (fun _ -> x)
     ```
     </p></details>

## OCaml Modules and Functors

1. Write a module signature `SetType` that declares a type `elem` and
   a type `t` where the values of `t` represent sets over values of
   type `elem`. Your signature should support the following
   operations:
   
   1. A value `empty` representing the empty set
   
   2. A function `add` for inserting an element into a set
   
   3. A function `remove` for removing an element from a set
   
   4. A function `mem` for checking whether a given element is a
      member of a given set.
      
   5. A function `fold` that implements a fold function on sets. For
      example, if the type `elem` is `int`, then 
      
      ```ocaml
      fold (fun acc x -> acc + x) 0 s
      ```
      
      should compute the sum of all the elements stored in the set `s`.

   <details><summary>Solution</summary>
   <p>

    ```ocaml
    module type SetType = sig
      type elem
      type t
      
      val empty: t
      val add: elem -> t -> t
      val remove: elem -> t -> t
      val mem: elem -> t -> bool
      val fold: ('a -> elem -> 'a) -> 'a -> t -> 'a
    end
    ```
   </p></details>

2. Consider the following module signature for ordered types:

   ```ocaml
   module type OrderedType =
     sig
       type t
       val compare : t -> t -> int
     end
   ```
   
   as well as the following algebraic data type for binary search trees:

   ```ocaml
   type tree = 
   | Leaf
   | Node of elem * tree * tree
   ```

   Write a functor that takes a module of type `OrderedType` and then
   uses the above binary search tree ADT to implement a module of type
   `SetType`:

   ```ocaml
   module MakeSet (O: OrderedType) : SetType with type elem = O.t = 
     struct
       type elem = O.t

       type tree = 
       | Leaf
       | Node of elem * tree * tree
       
       type t = tree
       ...
   end
   ```

   Implement `fold` using an in-order traversal of the tree.


   <details><summary>Solution</summary>
     <p>
     
     ```ocaml
     module MakeSet (O: OrderedType) : SetType with type elem = O.t = struct
       type elem = O.t
       
       type tree = 
       | Leaf
       | Node of elem * tree * tree
       
       type t = tree
      
       let empty = Leaf
      
       let rec mem x = function
         | Leaf -> false
         | Node (y, left, right) ->
           let cmp = O.compare x y in
           cmp = 0 || if cmp < 0 then mem x left else mem x right
      
       let rec add x = function
         | Leaf -> Node (x, Leaf, Leaf)
         | Node (y, left, right) as t ->
           let cmp = O.compare x y in
           if cmp = 0 then t else
           if cmp < 0 then Node (y, add x left, right)
           else Node (y, left, add x right)
          
       let rec delete_min = function
         | Node (min, Leaf, right) -> min, right
         | Node (x, left, right) -> 
           let min, mleft = delete_min left in
           min, Node (x, mleft, right)
         | Leaf -> assert false
      
       let rec remove x = function
         | Leaf -> Leaf
         | Node (y, left, right) ->
           let cmp = O.compare x y in
           if cmp = 0 then 
             match right with
             | Leaf -> left
             | _ -> 
               let rmin, right1 = delete_min right in
               Node (rmin, left, right1)
           else if cmp < 0 then 
             Node (y, remove x left, right)
           else
             Node (y, left, remove x right)
          
       let rec fold op z = function
         | Leaf -> z
         | Node (x, left, right) -> 
           let lres = fold op z left in
           fold op (op lres x) right
   end
   ```
   </p></details>

## Dynamic Dispatch

Consider the following Scala program:

```scala
class A:
  private def m1(s: String): A =
    println("A.m1(String)")
    new A
  
  def m2(): Unit = println("A.m2()")
  def m3(): A = 
    println("A.m3()")
    new A

object A:
  def m(a: A): A = a.m1("Hello")

class B extends A:
  private def m1(s: String): B =
    println("B.m1(String)")
    this
  
  override def m2(): Unit = println("B.m2()")
  
  override def m3(): A = 
    println("B.m3()")
    this

object Overriding extends App:
  val a1: A = new B

  val a2: A = A.m(a1)

  a2.m2()

  val a3: A = a1.m3()

  a3.m2()
```

1. What is the dynamic type of the variables `a1`, `a2`, and `a3` in
   `Overriding`?

   <details><summary>Solution</summary>
    <p>
    
    * `a1: B`. This is because we create a new `B` instance, whose reference we
      then assign to `a1`.
    
    * `a2: A`. This is because when method `m` of `A`'s companion
      object calls `m1` on the passed instance `a1`, the call will go
      to `A.m1` because `m1` is private and we are in the companion
      object of `A`. The call to `A.m1` returns the reference of a new
      `A` instance, which we then assign to `a2`.
      
    * `a3: B`. This is because the dynamic type of `a1` is `B` and `B`
      overrides `m3`, so the call goes to `B.m3`, which returns
      `this`, i.e. `a1`. Thus, `a3` and `a1` will alias the same `B`
      instance.

    </p></details>

1. What does each of the four method calls in `Overriding` print when
   it is executed? Explain.

   <details><summary>Solution</summary>
    <p>
    
    * `A.m(a1)`: this prints `A.m1(String)` because the `A.m` calls
      `A.m1` (see above).
      
    * `a2.m2()`: this prints `A.m2()` because the dynamic type of `a2`
      is `A` and the call goes to `A.m2`.
      
    * `a1.m3()`: this prints `B.m3()` because the dynamic type of `a1`
      is `B` and `B` overrides `A.m3`. Hence, the call goes to `B.m3`.
      
    * `a3.m2()`: this prints `B.m2()` because the dynamic type of `a3`
      is `B` and `B` overrides `A.m2`. Hence, the call goes to `B.m2`.

    </p></details>

## Data Layouts and Vtables

Consider the following Scala classes.

```scala
class Base(private val name: String, val c: Char):
  
  override def toString: String = name
  
  def m1(o: Any): Any =
    println("Base.m1(Any)")
    o
  
  def m2(o: Base): Unit = println("Base.m2(Base)")
  
  private def m3(s: String): Unit = println("Base.m3(String)")

class Derived(val x: Int, val name: String) extends Base(name, 'c'):
  private val y: Int = 0
 
  override def m1(o: Any): Derived =
    println("Derived.m1(Any)") 
    this
  
  def m4(o: Derived): Unit = println("Derived.m4(Derived)")
```

1. What are the correctly ordered entries in `Derived`'s data layout and vtable? Please use
   ```scala
   <classname>.<fieldname> : <type>
   ```
   notation for data layout entries, and
   
   ```scala
   <classname>.<methodname>(<type>, ..., <type>): <type>
   ```
   notation for vtable entries. Here, `<classname>` refers to the name
   of the class where the field, respectively, method has been
   declared. For simplicity, you may assume that the only method that
   `Base` inherits from `AnyRef` is `toString`.

   <details><summary>Solution</summary>
    <p>
    
    Data layout of `Derived`
    ```scala
    Base.name: String
    Base.c: Char
    Derived.x: Int
    Derived.name: String
    Derived.y: Int
    ```
    
    Vtable of `Derived`
    ```scala
    Base.toString: String
    Derived.m1(Any): Derived 
    Base.m2(Base): Unit
    Derived.m4(Derived): Unit
    ```

    </p></details>

## Scala Generics

Consider the following two generic Scala classes:

```scala
class CoVar[+T](x: T):
  def method1: T = x
  def method2(y: T): List[T] = List(x,y)

class ContraVar[-T](x: T):
  def method1: T = x
  def method2(y: T): List[T] = List(x,y)
```

The Scala compiler will reject both classes because at least one
method in each class violates the variance annotation of the type
parameter `T` of that class because the type occurs in a position with
opposite variance.

1. For each class, indicate the occurrences of the type parameter in
   the code that violates the variance annotation.
   
1. Change each class such that the violations of variances are
   fixed. You are _not allowed_ to change any of the following:

   * the variance annotation of the type parameter T
   * the type of the class parameter `x`;
   * the parameter names and implementations of the methods.

   However, you are allowed to introduce additional generic type
   parameters and type bounds to individual methods or the entire
   class. You are also allowed to change the parameter types and
   return types of methods. If you change any of the methods' types,
   the types should remain as precise as possible (e.g., you are not
   allowed to use the types `Any` or `Nothing`). 
   
   Your resulting code needs to be well-typed.
   
Hints:
  
* Recall that the type `List[A]` is covariant in `A`.

* You might find it more difficult to fix the class `ContraVar`. Note
  that you can introduce an additional type parameter for the whole
  class to replace the violating occurrences of `T` and then use a
  type bound to bound this new parameter appropriately using `T`.

<details><summary>Solution</summary>
  <p>
  
  ```scala
  class CoVar[+T](x: T):
    def method1: T = x
    def method2[U >: T](y: U): List[U] = List(x,y)

  class ContraVar[-T, +U >: T](x: T):
    def method1: U = x
    def method2(y: T): List[U] = List(x,y)
  ```
  </p></details>

## Memory Management

Consider the following C++ program:
```C++
 1: #include "ptr.h"
 2: 
 3: struct A;
 4:
 5: struct B {
 6:   Ptr<A> a;
 7:   B(Ptr<A>& _a) : a(_a) { }
 8:   B(A* _a) : a(_a) { }
 9: };
10:
11: struct A {
12:   Ptr<B> b;
13:   A(Ptr<B>& _b) : b(_b) { }
14: };
15:
16: int main(void) {
17:   Ptr<B> pn = 0;
18:
19:   Ptr<B> pb = new B(0);
20:
21:   Ptr<A> pa = new A(pb);
22:
23:   pb->a = pa;
24:
25:   pa->b = pn;
26:
27:   return 0;
28: }
```

Here, we assume the implementation of `Ptr` from [Class 13](https://github.com/nyu-pl-sp19/class13/blob/master/src/ptr.h).

1. When we trace the execution of this program, we observe that the following
   methods (respectively constructors and destructors) are called in
   the given order:
  
   ```c++
   Ptr<B>(B*)
   B(A*)
   Ptr<A>(A*)
   Ptr<B>(B*)
   A(Ptr<B>&)
   Ptr<B>(const Ptr<B>&)
   Ptr<A>(A*)
   Ptr<B>::operator->()
   Ptr<A>::operator=(const Ptr<A>&)
   Ptr<A>::operator->()
   Ptr<B>::operator=(const Ptr<B>&)
   ~Ptr<A>
   ~Ptr<B>
   ~B
   ~Ptr<A>
   ~A
   ~Ptr<B>
   ~Ptr<B>
   ```
  
   For each call, explain where the call is coming from. Here is an
   example for the first entry:
  
   `Ptr<B>(B*)` Call to `Ptr` constructor when `pn` is initialized on
   line 17.
  
   Note that some of the method calls happen on the same line in the program.

      <details><summary>Solution</summary>
    <p>
    
    * `Ptr<B>(B*)`: Call to `Ptr` constructor when `pn` is initialized on
      line 17.
      
    * `B(A*)`: Call to `B` constructor when `B` instance is created on
      line 19`.

    * `Ptr<A>(A*)`: Call to `Ptr` constructor when `a` field of `B` is
      initialized on line 8.
   
    * `Ptr<B>(B*)`: Call to `Ptr` constructor when `pb` is initialized on
      line 19.
      
    * `A(Ptr<B>&)`: Call to `A` constructor when `A` instance is created on
      line 21.
      
    * `Ptr<B>(const Ptr<B>&)`:  Call to `Ptr` copy constructor when `b` field of `A` is
      initialized on line 13.
      
    * `Ptr<A>(A*)` Call to `Ptr` constructor when `pa` is initialized on line 21.

    * `Ptr<B>::operator->()`: Call to arrow operator of `Ptr` when `pb->a` is
      executed on line 23.
   
    * `Ptr<A>::operator=(const Ptr<A>&)`: Call to assignment operator
      of `Ptr` when assignment to `pb->a` is executed on line 23.
   
    * `Ptr<A>::operator->()`: Call to arrow operator of `Ptr` when `pa->b` is
      executed on line 25.
    
    * `Ptr<B>::operator=(const Ptr<B>&)`: Call to assignment operator
      of `Ptr` when assignment to `pa->b` is executed on line 25.

    * `~Ptr<A>`: Call to `Ptr` destructor when `pa` is popped from the
      stack on line 27.

    * `~Ptr<B>`: Call to `Ptr` destructor when `pb` is popped from the
      stack on line 27.
 
    * `~B`: Call to `~B` destructor from within `~Ptr<B>` destructor
      of `pb` when deleting `*pb`.
   
    * `~Ptr<A>`: Call to `Ptr` destructor for field `a` of `*pb` from within `B` destructor.

    * `~A`: Call to `A` destructor from within `Ptr` destructor for
      field `a` when deleting `pb->a`.
  
    * `~Ptr<B>`: Call to `Ptr` destructor for field `b` of `pb->a`
      from within `A` destructor.
   
    * `~Ptr<B>`: Call to `Ptr` destructor when `pn` is popped from the
      stack on line 27.
    </p></details>

1. Draw diagrams that illustrate the memory state of the program
   (including the stack and heap contents) right before each of the
   following lines in the program is executed:
   
   * line 25
   
   * line 27

   <details><summary>Solution</summary>
     <p>
     See <a target="_blank" href="ptr-trace.pdf">here</a>.
     </p>
   </details>

# Normal Forms and Curry-Howard Isomorphism

* Untyped λ Calculus
* Simply Typed λ Calculus

Term with non-terminating sequence of reductions:

	(λ x . x x) (λ y . y y)
	 ↝ [x↦(λ y . y y)](x x)
	 = (λ y . y y) (λ y . y y)
	 ↝ [y↦(λ y . y y)](y y)
	 = (λ y . y y) (λ y . y y)
	 ↝ [y↦(λ y . y y)](y y)
	 = (λ y . y y) (λ y . y y)
	 ↝ [y↦(λ y . y y)](y y)
	 = (λ y . y y) (λ y . y y)
	 ↝ [y↦(λ y . y y)](y y)
	 = (λ y . y y) (λ y . y y)
	 ↝ [y↦(λ y . y y)](y y)
	 = (λ y . y y) (λ y . y y)
	 ...

Term with non-terminating sequence of reductions *but* has a normal form!

     (λ x . a) ((λ y . y y) (λ y . y y))
     ↝ a

     (λ x . a) ((λ y . y y) (λ y . y y))
     ↝ (λ x . a) ((λ y . y y) (λ y . y y))
     ↝ (λ x . a) ((λ y . y y) (λ y . y y))
     ↝ (λ x . a) ((λ y . y y) (λ y . y y))
     ↝ (λ x . a) ((λ y . y y) (λ y . y y))
     ↝ (λ x . a) ((λ y . y y) (λ y . y y))
     ↝ (λ x . a) ((λ y . y y) (λ y . y y))
     ↝ (λ x . a) ((λ y . y y) (λ y . y y))
     ↝ a

**Definition:** a term is *in normal form* if no reductions apply.

**Definition:** a λ calculus is *confluent* if:

Given some term e, and two reduction sequences

    e ↝...↝ e1
    e ↝...↝ e2

there exists a term e3 and reduction sequences

    e1 ↝...↝ e3
    e2 ↝...↝ e3

This is the *diamond property*.

If a λ calculus is *confluent* then it is *normalizing*.

**Theorem:** The Simply Typed λ Calculus is *strongly normalizing*.
I.e., no infinite chains of reductions.

The Curry-Howard Isomorphism says:

- Type inference is logic inference (plus stuff).
````
Γ ⊢ e1 : A → B          Γ ⊢ e2 : A
----------------------------------
           Γ ⊢ e1 e2 : B
````
If we scribble out e1 and e2 (the terms) leaving just the types, we have the Modus Ponens rule.
````
Γ ⊢ A → B          Γ ⊢ A
------------------------
         Γ ⊢ B
````

- Types are Predicate Calculus Theorems

  Take ```e = (λ f . λ g . λ x . f ( g x ))``` applied to the three arguments ```isZero round π```.

  Which has the type ```e : (int → bool) → (ℝ → int) -> ℝ -> bool```.
  Considered as a logic statement instead of a type, this is a tautology.

- Types of basis objects are axioms.
````
	 (b ↦ T) ∈ Γ
	 ---------
	 Γ ⊢ b : T
````
Existence of term of type ```T``` is a proof of the logical statement ```T```.

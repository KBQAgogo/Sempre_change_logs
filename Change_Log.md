# Date and changes

### Apr 2 
-- Bing

+ link /data/sempre/virtuoso-opensource to our new sempre1.0 folder
+ changed to tags/v1.0 and checkout to branch reproduce
+ ./download-dependencies emnlp2013   
./download-dependencies fullfreebase_vdb

-- Ma

a few problems: 
1. @mode=simple-freebase SimpleLexiconFn has runtime error;  
   there is an online issue about the reason: https://github.com/percyliang/sempre/issues/76; but setup local Virtuoso instance cannot      solve;
2. thinking about new features; 

### Apr 6
-- Ma

code reading:
--- Builder
			--- grammar
			--- executor 
			--- extractor: FeatureExtractor.java
								--- add feature:
										1. Add FeatureExtractor classes, which are called on each sub-Derivation.
										2. Use SemanticFn, which are called whenever they are called.
										(find all features: -FeatureExtractor.featureDomains basicStats alignmentScores tokensDistance context                                skipPos joinPos wordSim tokenMatch opCount constant denotation whType lexAlign)
			--- parser
--- Dataset
--- Learner

next step: need to find out how those features are extracted while training the data; 




### Apr 7

--bing

#### Possible improvement points from paper ??
+ "For unary predicates, we consider all logical forms Type.t and Profession.t for all (abstract) entities t.... The types of logical predicates considered during alignment is restricted in this paper, bu automatic induction of more compositional logical predicates is an interesting direction..." 
+ "Given the phrase r1 and the Freebase name s2 of the predicate r2, we compute string similarity features such as whether r1 and s2 are equal as well as some other measres of token overlap.."   
Possible to involve a threshold of word distance here??

#### Code
SemanticFun.java


```java
// Main entry point: given information the arguments of the SemanticFn,
  // return a list of Derivations.
  public abstract List<Derivation> call(Example ex, Callable c);
```

Derivation implements SemanticFun.Callable    

so we can call derivation addFeature()  to add the feature we want to impose on the specific derivation. 
  
  
  
```java
  // Functions that operate on features.
  public void addFeature(String domain, String name) { addFeature(domain, name, 1); }
  public void addFeature(String domain, String name, double value) { this.localFeatureVector.add(domain, name, value); }
  public void addFeatureWithBias(String domain, String name, double value) { this.localFeatureVector.addWithBias(domain, name, value); }
  public void addFeatures(FeatureVector fv) { this.localFeatureVector.add(fv); }
  public void addFeatures(Derivation deriv) { this.localFeatureVector.add(deriv.localFeatureVector); }
  
```

Then the when the score of the derivation is computed, these features are used to do the dot product   

Tmr need to run the system and reproduce the experiment data firstly....gogo




## Apr 20
+ Added SVM.java to the project which hasn't been completed and tested.
+ The TODO parts needs reconsideration or finishing.
+ Slightly modified Params.java and Learner.java

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

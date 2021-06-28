# **StackOverflow profiling**
![](https://user-images.githubusercontent.com/40482520/123009832-b9b43d00-d37a-11eb-9c9f-fb83d1a21a6c.png)

------------
1. [Introduction to business logic](#introduction-business)
2. [Description of the dataset and data dictionary of the dataset](#description-dataset)
3. [Data profiling results](#data-profiling)
4. [Specification of analytical needs that the proposed model will solve](#specification-to-solve)
5. [Proposed dimensional model](#dimensional-model)
6. [Mapping by table](#mapping)

<a name="introduction-business"></a>
## Introduction to business logic

<a name="description-dataset"></a>
## Description of the dataset and data dictionary of the dataset
A continuación describiremos con más detalles cada una de las tablas que conforman nuestro dataset de StackOverflow:

| N° |Table name   |Number of records   |Size   |  column | Used for MD  |
| ------------ | ------------ | ------------ | ------------| ------------ | ------------ |
| 1  | badges   |  39,178,976 | 1.78 GB  |  6 |Yes   |
|   2|  comments  |  79,220,809 | 16.64 GB  | 7  |No   |
|   3|  posts_answers  | 31,169,249  | 27.6 GB |20   | Yes  |
|   4|  posts_moderator_nomination  |  334 | 473.5 KB  |20  |No   |
|   5| posts_orphaned_tag_wiki   | 167  |53.34 KB   |20   |No   |
|   6|  post_history |138,808,451   | 109.24 GB  | 8  |Yes   |
|   7|   post_links | 7,302,589  |291.1 MB   |  5 |No   |
|   8| users   | 14,080,580  | 2.4 GB  |13   |Yes   |
|   9|  posts_privilege_wiki  |  2 | 3.49 KB  | 20  |No   |
|   10| posts_questions   | 20,890,054  |35.58 GB   |20   |Yes   |
|   11|  posts_tag_wiki  |53036   |36.57 MB   |20   | Yes  |
|   12|  posts_tag_wiki_excerpt  |53036   | 11.02 MB  | 20  |No   |
|   13|  posts_wiki_placeholder  | 5  | 5.63 KB  |20   | No  |
|   14| stackoverflow_posts   |31,017,889   | 31.52 GB  |20   | Yes  |
|   15| tags   |60,534   | 2.48 MB  | 5  | Yes  |
|   16|   votes|208,577,841   | 6.67 GB  |4   | Yes  ||

<a name="data-profiling"></a>
## Data profiling results

<a name="specification-to-solve"></a>
## Specification of analytical needs that the proposed model will solve

<a name="dimensional-model"></a>
## Proposed dimensional model

<a name="mapping"></a>
## Mapping by table



# 1. **StackOverflow profiling**

![](https://user-images.githubusercontent.com/40482520/123009832-b9b43d00-d37a-11eb-9c9f-fb83d1a21a6c.png)

------------

- [1. **StackOverflow profiling**](#1-stackoverflow-profiling)
  - [1.1. Introduction to business logic](#11-introduction-to-business-logic)
  - [1.2. Description of the dataset and data dictionary of the dataset](#12-description-of-the-dataset-and-data-dictionary-of-the-dataset)
    - [1.2.1. Description](#121-description)
    - [1.2.2. Data dictionary](#122-data-dictionary)
      - [1.2.2.1. Source: Big Query](#1221-source-big-query)
        - [1.2.2.1.1. badges](#12211-badges)
        - [1.2.2.1.2. comments](#12212-comments)
        - [1.2.2.1.3. posts_answers](#12213-posts_answers)
        - [1.2.2.1.4. posts_moderator_nomination](#12214-posts_moderator_nomination)
        - [1.2.2.1.5. posts_orphaned_tag_wiki](#12215-posts_orphaned_tag_wiki)
        - [1.2.2.1.6. post_history](#12216-post_history)
        - [1.2.2.1.7. post_links](#12217-post_links)
        - [1.2.2.1.8. users](#12218-users)
        - [1.2.2.1.9. posts_privilege_wiki](#12219-posts_privilege_wiki)
        - [1.2.2.1.10. posts_questions](#122110-posts_questions)
        - [1.2.2.1.11. posts_tag_wiki](#122111-posts_tag_wiki)
        - [1.2.2.1.12. posts_tag_wiki_excerpt](#122112-posts_tag_wiki_excerpt)
        - [1.2.2.1.13. posts_wiki_placeholder](#122113-posts_wiki_placeholder)
        - [1.2.2.1.14. stackoverflow_posts](#122114-stackoverflow_posts)
        - [1.2.2.1.15. tags](#122115-tags)
        - [1.2.2.1.16. votes](#122116-votes)
      - [1.2.2.2. Source: XML](#1222-source-xml)
        - [1.2.2.2.1. badges](#12221-badges)
        - [1.2.2.2.2. comments](#12222-comments)
        - [1.2.2.2.3. postHistory](#12223-posthistory)
        - [1.2.2.2.4. postLink](#12224-postlink)
        - [1.2.2.2.5. post](#12225-post)
        - [1.2.2.2.6. tags](#12226-tags)
        - [1.2.2.2.7. user](#12227-user)
        - [1.2.2.2.8. view_archive_cleaner](#12228-view_archive_cleaner)
        - [1.2.2.2.9. votes](#12229-votes)
  - [1.3. Data profiling results](#13-data-profiling-results)
    - [1.3.1. Source: Big Query](#131-source-big-query)
      - [1.3.1.1. badges](#1311-badges)
      - [1.3.1.2. comments](#1312-comments)
      - [1.3.1.3. posts_answers](#1313-posts_answers)
      - [1.3.1.4. posts_moderator_nomination](#1314-posts_moderator_nomination)
      - [1.3.1.5. posts_orphaned_tag_wiki](#1315-posts_orphaned_tag_wiki)
      - [1.3.1.6. post_history](#1316-post_history)
      - [1.3.1.7. post_links](#1317-post_links)
      - [1.3.1.8. users](#1318-users)
      - [1.3.1.9. posts_privilege_wiki](#1319-posts_privilege_wiki)
      - [1.3.1.10. posts_questions](#13110-posts_questions)
      - [1.3.1.11. posts_tag_wiki](#13111-posts_tag_wiki)
      - [1.3.1.12. posts_tag_wiki_excerpt](#13112-posts_tag_wiki_excerpt)
      - [1.3.1.13. posts_wiki_placeholder](#13113-posts_wiki_placeholder)
      - [1.3.1.14. stackoverflow_posts](#13114-stackoverflow_posts)
      - [1.3.1.15. tags](#13115-tags)
      - [1.3.1.16. votes](#13116-votes)
    - [1.3.2. Source: XML](#132-source-xml)
      - [1.3.2.1. badges](#1321-badges)
      - [1.3.2.2. comments](#1322-comments)
      - [1.3.2.3. postHistory](#1323-posthistory)
      - [1.3.2.4. postLink](#1324-postlink)
      - [1.3.2.5. post](#1325-post)
      - [1.3.2.6. tags](#1326-tags)
      - [1.3.2.7. user](#1327-user)
      - [1.3.2.8. view_archive_cleaner](#1328-view_archive_cleaner)
      - [1.3.2.9. votes](#1329-votes)
  - [1.4. Specification of analytical needs that the proposed model will solve](#14-specification-of-analytical-needs-that-the-proposed-model-will-solve)
  - [1.5. Proposed dimensional model](#15-proposed-dimensional-model)
  - [1.6. Mapping by table](#16-mapping-by-table)
    - [1.6.1. Dim_Question](#161-dim_question)
    - [1.6.2. Dim_user](#162-dim_user)
    - [1.6.3. Dim_tag](#163-dim_tag)
    - [1.6.4. Dim_tag_bridge](#164-dim_tag_bridge)
    - [1.6.5. Dim_Time](#165-dim_time)
    - [1.6.6. Dim_Date](#166-dim_date)
    - [1.6.7. Fact_Done_Question](#167-fact_done_question)
    - [1.6.8. Fact_Done_Answer](#168-fact_done_answer)

## 1.1. Introduction to business logic

## 1.2. Description of the dataset and data dictionary of the dataset

### 1.2.1. Description

A continuación describiremos con más detalles cada una de las tablas que conforman nuestro dataset de StackOverflow:

| N°  | Table name                 | Number of records | Size      | column | Used for MD |
| --- | -------------------------- | ----------------- | --------- | ------ | ----------- |
| 1   | badges                     | 39,178,976        | 1.78 GB   | 6      | Yes         |
| 2   | comments                   | 79,220,809        | 16.64 GB  | 7      | No          |
| 3   | posts_answers              | 31,169,249        | 27.6 GB   | 20     | Yes         |
| 4   | posts_moderator_nomination | 334               | 473.5 KB  | 20     | No          |
| 5   | posts_orphaned_tag_wiki    | 167               | 53.34 KB  | 20     | No          |
| 6   | post_history               | 138,808,451       | 109.24 GB | 8      | Yes         |
| 7   | post_links                 | 7,302,589         | 291.1 MB  | 5      | No          |
| 8   | users                      | 14,080,580        | 2.4 GB    | 13     | Yes         |
| 9   | posts_privilege_wiki       | 2                 | 3.49 KB   | 20     | No          |
| 10  | posts_questions            | 20,890,054        | 35.58 GB  | 20     | Yes         |
| 11  | posts_tag_wiki             | 53036             | 36.57 MB  | 20     | Yes         |
| 12  | posts_tag_wiki_excerpt     | 53036             | 11.02 MB  | 20     | No          |
| 13  | posts_wiki_placeholder     | 5                 | 5.63 KB   | 20     | No          |
| 14  | stackoverflow_posts        | 31,017,889        | 31.52 GB  | 20     | Yes         |
| 15  | tags                       | 60,534            | 2.48 MB   | 5      | Yes         |
| 16  | votes                      | 208,577,841       | 6.67 GB   | 4      | Yes         |

### 1.2.2. Data dictionary

#### 1.2.2.1. Source: Big Query

##### 1.2.2.1.1. badges

| Attribute name | Type | Is mandatory | Is mandatory | Is primary | Is foreign | Description |
| -------------- | ---- | ------------ | ------------ | ---------- | ---------- | ----------- |
|                |      |              |              |            |            |             |

##### 1.2.2.1.2. comments

| Attribute name | Type | Is mandatory | Is mandatory | Is primary | Is foreign | Description |
| -------------- | ---- | ------------ | ------------ | ---------- | ---------- | ----------- |
|                |      |              |              |            |            |             |

##### 1.2.2.1.3. posts_answers

| Attribute name | Type | Is mandatory | Is mandatory | Is primary | Is foreign | Description |
| -------------- | ---- | ------------ | ------------ | ---------- | ---------- | ----------- |
|                |      |              |              |            |            |             |

##### 1.2.2.1.4. posts_moderator_nomination

| Attribute name | Type | Is mandatory | Is mandatory | Is primary | Is foreign | Description |
| -------------- | ---- | ------------ | ------------ | ---------- | ---------- | ----------- |
|                |      |              |              |            |            |             |

##### 1.2.2.1.5. posts_orphaned_tag_wiki

| Attribute name | Type | Is mandatory | Is mandatory | Is primary | Is foreign | Description |
| -------------- | ---- | ------------ | ------------ | ---------- | ---------- | ----------- |
|                |      |              |              |            |            |             |

##### 1.2.2.1.6. post_history

| Attribute name | Type | Is mandatory | Is mandatory | Is primary | Is foreign | Description |
| -------------- | ---- | ------------ | ------------ | ---------- | ---------- | ----------- |
|                |      |              |              |            |            |             |

##### 1.2.2.1.7. post_links

| Attribute name | Type | Is mandatory | Is mandatory | Is primary | Is foreign | Description |
| -------------- | ---- | ------------ | ------------ | ---------- | ---------- | ----------- |
|                |      |              |              |            |            |             |

##### 1.2.2.1.8. users

| Attribute name | Type | Is mandatory | Is mandatory | Is primary | Is foreign | Description |
| -------------- | ---- | ------------ | ------------ | ---------- | ---------- | ----------- |
|                |      |              |              |            |            |             |

##### 1.2.2.1.9. posts_privilege_wiki

| Attribute name | Type | Is mandatory | Is mandatory | Is primary | Is foreign | Description |
| -------------- | ---- | ------------ | ------------ | ---------- | ---------- | ----------- |
|                |      |              |              |            |            |             |

##### 1.2.2.1.10. posts_questions

| Attribute name | Type | Is mandatory | Is mandatory | Is primary | Is foreign | Description |
| -------------- | ---- | ------------ | ------------ | ---------- | ---------- | ----------- |
|                |      |              |              |            |            |             |

##### 1.2.2.1.11. posts_tag_wiki

| Attribute name | Type | Is mandatory | Is mandatory | Is primary | Is foreign | Description |
| -------------- | ---- | ------------ | ------------ | ---------- | ---------- | ----------- |
|                |      |              |              |            |            |             |

##### 1.2.2.1.12. posts_tag_wiki_excerpt

| Attribute name | Type | Is mandatory | Is mandatory | Is primary | Is foreign | Description |
| -------------- | ---- | ------------ | ------------ | ---------- | ---------- | ----------- |
|                |      |              |              |            |            |             |

##### 1.2.2.1.13. posts_wiki_placeholder

| Attribute name | Type | Is mandatory | Is mandatory | Is primary | Is foreign | Description |
| -------------- | ---- | ------------ | ------------ | ---------- | ---------- | ----------- |
|                |      |              |              |            |            |             |

##### 1.2.2.1.14. stackoverflow_posts

| Attribute name | Type | Is mandatory | Is mandatory | Is primary | Is foreign | Description |
| -------------- | ---- | ------------ | ------------ | ---------- | ---------- | ----------- |
|                |      |              |              |            |            |             |

##### 1.2.2.1.15. tags

| Attribute name | Type | Is mandatory | Is mandatory | Is primary | Is foreign | Description |
| -------------- | ---- | ------------ | ------------ | ---------- | ---------- | ----------- |
|                |      |              |              |            |            |             |

##### 1.2.2.1.16. votes

| Attribute name | Type | Is mandatory | Is mandatory | Is primary | Is foreign | Description |
| -------------- | ---- | ------------ | ------------ | ---------- | ---------- | ----------- |
|                |      |              |              |            |            |             |

#### 1.2.2.2. Source: XML

##### 1.2.2.2.1. badges

| Attribute name | Type | Is mandatory | Is mandatory | Is primary | Is foreign | Description |
| -------------- | ---- | ------------ | ------------ | ---------- | ---------- | ----------- |
|                |      |              |              |            |            |             |

##### 1.2.2.2.2. comments

| Attribute name | Type | Is mandatory | Is mandatory | Is primary | Is foreign | Description |
| -------------- | ---- | ------------ | ------------ | ---------- | ---------- | ----------- |
|                |      |              |              |            |            |             |

##### 1.2.2.2.3. postHistory

| Attribute name | Type | Is mandatory | Is mandatory | Is primary | Is foreign | Description |
| -------------- | ---- | ------------ | ------------ | ---------- | ---------- | ----------- |
|                |      |              |              |            |            |             |

##### 1.2.2.2.4. postLink

| Attribute name | Type | Is mandatory | Is mandatory | Is primary | Is foreign | Description |
| -------------- | ---- | ------------ | ------------ | ---------- | ---------- | ----------- |
|                |      |              |              |            |            |             |

##### 1.2.2.2.5. post

| Attribute name | Type | Is mandatory | Is mandatory | Is primary | Is foreign | Description |
| -------------- | ---- | ------------ | ------------ | ---------- | ---------- | ----------- |
|                |      |              |              |            |            |             |

##### 1.2.2.2.6. tags

| Attribute name | Type | Is mandatory | Is mandatory | Is primary | Is foreign | Description |
| -------------- | ---- | ------------ | ------------ | ---------- | ---------- | ----------- |
|                |      |              |              |            |            |             |

##### 1.2.2.2.7. user

| Attribute name | Type | Is mandatory | Is mandatory | Is primary | Is foreign | Description |
| -------------- | ---- | ------------ | ------------ | ---------- | ---------- | ----------- |
|                |      |              |              |            |            |             |

##### 1.2.2.2.8. view_archive_cleaner

| Attribute name | Type | Is mandatory | Is mandatory | Is primary | Is foreign | Description |
| -------------- | ---- | ------------ | ------------ | ---------- | ---------- | ----------- |
|                |      |              |              |            |            |             |

##### 1.2.2.2.9. votes

| Attribute name | Type | Is mandatory | Is mandatory | Is primary | Is foreign | Description |
| -------------- | ---- | ------------ | ------------ | ---------- | ---------- | ----------- |
|                |      |              |              |            |            |             |

## 1.3. Data profiling results

### 1.3.1. Source: Big Query

#### 1.3.1.1. badges

| Attribute name | Type | Proportion of valid (valid / total) | Result | Conclusion |
| -------------- | ---- | ----------------------------------- | ------ | ---------- |
|                |      |                                     |        |            |

#### 1.3.1.2. comments

| Attribute name | Type | Proportion of valid (valid / total) | Result | Conclusion |
| -------------- | ---- | ----------------------------------- | ------ | ---------- |
|                |      |                                     |        |            |

#### 1.3.1.3. posts_answers

| Attribute name | Type | Proportion of valid (valid / total) | Result | Conclusion |
| -------------- | ---- | ----------------------------------- | ------ | ---------- |
|                |      |                                     |        |            |

#### 1.3.1.4. posts_moderator_nomination

| Attribute name | Type | Proportion of valid (valid / total) | Result | Conclusion |
| -------------- | ---- | ----------------------------------- | ------ | ---------- |
|                |      |                                     |        |            |

#### 1.3.1.5. posts_orphaned_tag_wiki

| Attribute name | Type | Proportion of valid (valid / total) | Result | Conclusion |
| -------------- | ---- | ----------------------------------- | ------ | ---------- |
|                |      |                                     |        |            |

#### 1.3.1.6. post_history

| Attribute name | Type | Proportion of valid (valid / total) | Result | Conclusion |
| -------------- | ---- | ----------------------------------- | ------ | ---------- |
|                |      |                                     |        |            |

#### 1.3.1.7. post_links

| Attribute name | Type | Proportion of valid (valid / total) | Result | Conclusion |
| -------------- | ---- | ----------------------------------- | ------ | ---------- |
|                |      |                                     |        |            |

#### 1.3.1.8. users

| Attribute name | Type | Proportion of valid (valid / total) | Result | Conclusion |
| -------------- | ---- | ----------------------------------- | ------ | ---------- |
|                |      |                                     |        |            |

#### 1.3.1.9. posts_privilege_wiki

| Attribute name | Type | Proportion of valid (valid / total) | Result | Conclusion |
| -------------- | ---- | ----------------------------------- | ------ | ---------- |
|                |      |                                     |        |            |

#### 1.3.1.10. posts_questions

| Attribute name | Type | Proportion of valid (valid / total) | Result | Conclusion |
| -------------- | ---- | ----------------------------------- | ------ | ---------- |
|                |      |                                     |        |            |

#### 1.3.1.11. posts_tag_wiki

| Attribute name | Type | Proportion of valid (valid / total) | Result | Conclusion |
| -------------- | ---- | ----------------------------------- | ------ | ---------- |
|                |      |                                     |        |            |

#### 1.3.1.12. posts_tag_wiki_excerpt

| Attribute name | Type | Proportion of valid (valid / total) | Result | Conclusion |
| -------------- | ---- | ----------------------------------- | ------ | ---------- |
|                |      |                                     |        |            |

#### 1.3.1.13. posts_wiki_placeholder

| Attribute name | Type | Proportion of valid (valid / total) | Result | Conclusion |
| -------------- | ---- | ----------------------------------- | ------ | ---------- |
|                |      |                                     |        |            |

#### 1.3.1.14. stackoverflow_posts

| Attribute name | Type | Proportion of valid (valid / total) | Result | Conclusion |
| -------------- | ---- | ----------------------------------- | ------ | ---------- |
|                |      |                                     |        |            |

#### 1.3.1.15. tags

| Attribute name | Type | Proportion of valid (valid / total) | Result | Conclusion |
| -------------- | ---- | ----------------------------------- | ------ | ---------- |
|                |      |                                     |        |            |

#### 1.3.1.16. votes

| Attribute name | Type | Proportion of valid (valid / total) | Result | Conclusion |
| -------------- | ---- | ----------------------------------- | ------ | ---------- |
|                |      |                                     |        |            |

### 1.3.2. Source: XML

#### 1.3.2.1. badges

| Attribute name | Type | Proportion of valid (valid / total) | Result | Conclusion |
| -------------- | ---- | ----------------------------------- | ------ | ---------- |
|                |      |                                     |        |            |

#### 1.3.2.2. comments

| Attribute name | Type | Proportion of valid (valid / total) | Result | Conclusion |
| -------------- | ---- | ----------------------------------- | ------ | ---------- |
|                |      |                                     |        |            |

#### 1.3.2.3. postHistory

| Attribute name | Type | Proportion of valid (valid / total) | Result | Conclusion |
| -------------- | ---- | ----------------------------------- | ------ | ---------- |
|                |      |                                     |        |            |

#### 1.3.2.4. postLink

| Attribute name | Type | Proportion of valid (valid / total) | Result | Conclusion |
| -------------- | ---- | ----------------------------------- | ------ | ---------- |
|                |      |                                     |        |            |

#### 1.3.2.5. post

| Attribute name | Type | Proportion of valid (valid / total) | Result | Conclusion |
| -------------- | ---- | ----------------------------------- | ------ | ---------- |
|                |      |                                     |        |            |

#### 1.3.2.6. tags

| Attribute name | Type | Proportion of valid (valid / total) | Result | Conclusion |
| -------------- | ---- | ----------------------------------- | ------ | ---------- |
|                |      |                                     |        |            |

#### 1.3.2.7. user

| Attribute name | Type | Proportion of valid (valid / total) | Result | Conclusion |
| -------------- | ---- | ----------------------------------- | ------ | ---------- |
|                |      |                                     |        |            |

#### 1.3.2.8. view_archive_cleaner

| Attribute name | Type | Proportion of valid (valid / total) | Result | Conclusion |
| -------------- | ---- | ----------------------------------- | ------ | ---------- |
|                |      |                                     |        |            |

#### 1.3.2.9. votes

| Attribute name | Type | Proportion of valid (valid / total) | Result | Conclusion |
| -------------- | ---- | ----------------------------------- | ------ | ---------- |
|                |      |                                     |        |            |

## 1.4. Specification of analytical needs that the proposed model will solve

## 1.5. Proposed dimensional model

## 1.6. Mapping by table

### 1.6.1. Dim_Question

| Column name | Type | Source | Comment | Sample |
| ----------- | ---- | ------ | ------- | ------ |
|             |      |        |         |        |

### 1.6.2. Dim_user

| Column name | Type | Source | Comment | Sample |
| ----------- | ---- | ------ | ------- | ------ |
|             |      |        |         |        |

### 1.6.3. Dim_tag

| Column name | Type | Source | Comment | Sample |
| ----------- | ---- | ------ | ------- | ------ |
|             |      |        |         |        |

### 1.6.4. Dim_tag_bridge

| Column name | Type | Source | Comment | Sample |
| ----------- | ---- | ------ | ------- | ------ |
|             |      |        |         |        |

### 1.6.5. Dim_Time

| Column name | Type | Source | Comment | Sample |
| ----------- | ---- | ------ | ------- | ------ |
|             |      |        |         |        |

### 1.6.6. Dim_Date

| Column name | Type | Source | Comment | Sample |
| ----------- | ---- | ------ | ------- | ------ |
|             |      |        |         |        |

### 1.6.7. Fact_Done_Question

| Column name | Type | Source | Comment | Sample |
| ----------- | ---- | ------ | ------- | ------ |
|             |      |        |         |        |

### 1.6.8. Fact_Done_Answer

| Column name | Type | Source | Comment | Sample |
| ----------- | ---- | ------ | ------- | ------ |
|             |      |        |         |        |

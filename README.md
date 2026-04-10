# Cloud-Computing-Project

This repository contains a demonstration notebook and supporting code for serverless architecture designed to manage large-scale lip-reading datasets using manifest-based approach.

The notebook is for demonstration only and does not execute AWS services locally:

- demonstrates Lambda function logic  
- explains data transformation steps  
- documents the architecture implementation  

This project is based on the previous research:  
**Efficient Management of Large-Scale Lip-Reading Datasets Using Manifest-Based Serverless Architectures on AWS**

## Overview

Traditional lip-reading datasets duplicate frame data for each viseme classification scheme, which leads to:

- increased storage costs   
- reduced scalability
- redundant data 

This project introduces a manifest-based architecture where:

- frame data is stored once in Amazon S3;  
- JSON manifest files represent different viseme mappings;  
- serverless processing automates dataset transformation.  

## Architecture

The system is fully serverless and event-driven using the following AWS services:

- Amazon S3 – storage for frames, alignments and manifests  
- AWS Lambda – processing and transformation  
- Amazon DynamoDB – phoneme-to-viseme mapping storage  
- Amazon SQS (Dead-Letter Queue) – failure handling  
- API Gateway – real-time querying  


## Lambda Functions

### generate_viseme_manifest
Processes phoneme alignment files, retrieves mapping data from DynamoDB and generates JSON manifest files stored in S3.

### duplicate_frames_by_viseme
Implements the baseline file-based approach by duplicating frames into viseme folders for comparison.

### load_mapping_to_dynamodb
Loads phoneme-to-viseme mappings into DynamoDB to support fast search.

### search_viseme_mapping
Handles API requests and returns viseme mappings across multiple viseme classification systems.

## Data Flow

1. Alignment file uploaded to S3  
2. S3 event triggers Lambda function  
3. Lambda queries DynamoDB for mappings  
4. Manifest files are generated  
5. Results stored in S3  
6. API Gateway enables querying  

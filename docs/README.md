
# Cozy-DISPERS

## Computing queries

![](pictures/cozy-dispers-extended-schema.png?raw=true)

- `/conductor` - [Management of the request](conductor.md)
- `/conceptindexor` - [Select requested users Pt.1](concept-indexor.md)
- `/targetfinder` - [Select requested users Pt.2](target-finder.md)
- `/target` - [Request the selected users](target.md)
- `/dataaggregator` - [Aggregate Data](data-aggregator.md)

## Quick start to build a network adapted for Cozy-DISPERS

[Tutorial to initialize a few instances with and subscribe to Cozy-DISPERS](quick-start.md)

```bash
NB_COZY=15
DELETING_INSTANCE="false"
PATH_CSV_FILE="./data/instances.csv"
./create_instances_from_csv.sh $NB_COZY $DELETING_INSTANCE $PATH_CSV_FILE
./add_data_from_csv.sh $NB_COZY $PATH_CSV_FILE
./create_concepts_from_csv.sh
./subscribe_dispers_from_csv.sh $NB_COZY $PATH_CSV_FILE
```

## Keep a look on the query

ExecutionMetadata provides a way to follow the query from end to end. ExecutionMetadata are created by the Conductor at several special step of processes and are saved in the Conductor's database.

- Host
- Begining / ending time

ExecutionMetadata has got one function and 2 methods :

- `NewExecutionMetadata` to instanciate a new ExecutionMetadata
- `.SetTask(...)` to add a step
- `.EndExecution(...)` to close the metadata and update it in database

Metadata are saved in a dedicated database with the doctype io.cozy.execution.metadata. This database contains one document for each query. ExecutionMetadata can be retrieved with this request :

```http
GET dispers/conductor/query HTTP/1.1
Host: cozy.example.org
Content-Type: application/json
```

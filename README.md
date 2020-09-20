# dynamodb-local-playground

This repo contains a `docker-compose.yml` you can use to quickly create a local DynamoDB with a web-based Admin GUI.

We use [cnadiminti/dynamodb-local](https://hub.docker.com/r/cnadiminti/dynamodb-local) for DynamoDB and [aaronshaf/dynamodb-admin](https://hub.docker.com/r/aaronshaf/dynamodb-admin) for the Admin GUI.

## Usage

### Start

To start your local DynamoDB, run the following command from your terminal:

`docker-compose up -d`

See [docker-compose up docs](https://docs.docker.com/compose/reference/up/) for additional flags to the `up` command.

Other docker-compose commands you'll probably want to familiarize yourself with are:

- [down](https://docs.docker.com/compose/reference/down/)
- [start](https://docs.docker.com/compose/reference/start/)
- [stop](https://docs.docker.com/compose/reference/stop/)
- [restart](https://docs.docker.com/compose/reference/restart/)

### GUI

After you start everything up, you can access `dynamodb-admin` at http://localhost:8001.

![image](https://user-images.githubusercontent.com/357481/93713482-49963380-fb2a-11ea-8e61-d127fe5ab73b.png)

In addition, `dynamodb-local` includes a browser-based JavaScript shell that you can use to interact with the database. You can access the shell at `http://localhost:4567/shell`.

![dynamodb-local shell](https://user-images.githubusercontent.com/357481/93713856-a72b7f80-fb2c-11ea-96f8-3306560245c5.png)

The shell is a more powerful alternative to `dynamodb-admin`, but you need to write complete DynamoDB commands like you would with the AWS SDK for JavaScript.

You can also use the aws cli. For example, to list all the tables, you would run:

```sh
aws dynamodb list-tables --endpoint-url http://0.0.0.0:4567
```

### Persistence

By default, all data associated with your local DynamoDB will be deleted when your `dynamodb-local` container is removed, such as after you run `docker-compose down`. If you would rather persist your data, you can add a [`docker-compose.override.yml`](https://docs.docker.com/compose/reference/overview/) that provides a local volume configuration. An example [`docker-compose.override.yml`](./docker-compose.override-example.yml) is provided.

## Complementary Tools

- [NoSQL Workbench for Amazon DynamoDB](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/workbench.settingup.html) -- a unified visual IDE tool that provides data modeling, data visualization, and query development features to help you design, create, query, and manage DynamoDB tables.
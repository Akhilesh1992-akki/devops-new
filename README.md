import json
import boto3
# from helper1 import read_data
 
client = boto3.client('dynamodb')
 
def lambda_handler(event, context):
    # TODO implement
    if event['EventType'] == 'helper1':
        response = helper1(event, context)
    elif event['EventType'] == 'helper2':
        response = helper2(event, context)
 
    return response
def helper1(event, context):
    data = client.put_item(
    TableName='user_info',
    Item={
        'id': {
          'S': '04'
        },
        'Name': {
          'S': 'Akhilesh'
        },
        'Address': {
          'S': 'J, India'
        }
    }
    )
    response = {
      'statusCode': 200,
      'body': 'successfully created item!',
      'headers': {
        'Content-Type': 'application/json',
        'Access-Control-Allow-Origin': '*'
      },
    }
    return response
 
def helper2(event, context):
  data = client.scan(
    TableName='user_info'
  )
 
  response = {
      'statusCode': 200,
      'body': json.dumps(data),
      'headers': {
        'Content-Type': 'application/json',
        'Access-Control-Allow-Origin': '*'
      },
  }
 
  return response

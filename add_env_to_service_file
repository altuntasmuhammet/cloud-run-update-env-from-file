import argparse, sys

# Service file can be obtained 
# gcloud run services describe <SERVICE_NAME> --format export > service.yml

parser=argparse.ArgumentParser()

parser.add_argument('--env-file', help='Environment variables file in YAML format', required=True)
parser.add_argument('--service-file', help='Cloud Run service file in YAML format', required=True)
parser.add_argument('--out', help='Environment variables added service file name', required=True)

args=parser.parse_args()

env_file = args.env_file
service_file = args.service_file
output_file = args.out


import yaml
# Read environment data
with open(env_file, 'r') as f:
    env_data = yaml.load(f, Loader=yaml.FullLoader)

with open(service_file, 'r') as f:
    service_data = yaml.load(f, Loader=yaml.FullLoader)

env_list = []
for key, value in env_data.items():
    env_list += [{
        "name": key,
        'value': value
    }]

# Add env
service_data['spec']['template']['spec']['containers'][0]['env'] = env_list
# Change name for avoiding conflict when deploying
service_data['spec']['template']['metadata']['name'] = service_data['spec']['template']['metadata']['name'] + '-with-env'

with open(output_file, 'w') as file:
    yaml.dump(service_data, file)

# After obtaining new service file run below command in terminal
# gcloud beta run services replace <out>

# Module to create RDS
## Create a file module.tf and add the following
```
module "db" {
source = "chaglare/rds-instance/aws"
region = "us-east-1"
subnet_ids = [
  "subnet-e91e8ad7",
  "subnet-e3c4d4a9",
  "subnet-8080cddc"
]
security_group_name = "db"
allowed_hosts = [
"0.0.0.0/0"
]
db_name = "dbname"
engine = "mysql"
engine_version = "5.7"
instance_class = "db.t2.micro"
username = "foo"
password = "foobarbaz"
publicly_accessible = true
allocated_storage   = "20"
}
```

## Create another file output.tf and add the following
```
output "region" {
value = "${module.db.region}"
}
output "subnet_list" {
value = "${module.db.subnet_list}"
}
output "allows_hosts" {
value = "${module.db.allowed_hosts}"
}
output "DB_NAME" {
value = "${module.db.DB_NAME}"
}
```

# Run 
```
terraform init 
terraform apply
```

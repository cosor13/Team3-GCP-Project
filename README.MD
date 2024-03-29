Database
Google Cloud SQL is managed database service and it allows us to run MySQL, PosgreSQL on GCloud.

In Cloud Shell under your repo folder, create a folder DB and add terraform files in it - dbinstance.tf, variables.tf and provider.tf

In dbinstance.tf add your resources to create your database instance. Use google_sql_database_instance resource for this:

resource "google_sql_database_instance" "instance" {
name = var.config["name"]
region = var.config["region"]
database_version = var.config["database_version"]
settings {
	tier = var.config["tier"]
}
deletion_protection = var.config["deletion_protection"]}

In dbinstance.tf file add your resource to create your database inside db instance

resource "google_sql_database" "database" {
name = var.config["name"]
instance = google_sql_database_instance.instance.name
}

In variables.tf add your variables to make your resources more dynamic
Run terraform init, terraform apply to apply your changes
Check Gcloud and make sure your resources are created under team3-db-instance
In Google Console, you will be able to find your db instance's Public IP address and also Connection name
From SQL service, add a user to your database instance
You can connect to your db instance from Cloud Shell by using gcloud sql connect team3-db-instance --user=mammadova --quiet command
Connect to your database instance, use show databases; query and make sure your db is created. this db will be used for wordpress connection
If you see your db inside your db instance, you should be good. Move on

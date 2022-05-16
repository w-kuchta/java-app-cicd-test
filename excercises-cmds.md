
https://dashboard.ngrok.com/signup
Download for Linux
tar -xf ngrok-v3-stable-linux-amd64.tgz 
mv ngrok /usr/bin/
(albo export PATH="$HOME/bin:$PATH")
ngrok config add-authtoken 28qH8oJcwjT2BTjo591PBFkle14_6zwwX2LF71jEjjPXZEpMp
ngrok http 8081

# JAVA
https://www.jenkins.io/doc/tutorials/build-a-java-app-with-maven/


# Konta
Dostaliście, ale jeśli macie ochotę to możecie założyć swoje testowe i cisnąć na nich, bo tu macie mocno ograniczone. Ewentualnie jeśli nie teraz to na następne zajęcia na projekt

# WoW
Przygotowany workbook

# Vagrant czy lokalnie na ubuntu??
Jesli Vagrant to utworzyc pliki z credentialami w
.vagrant-provisioning/aws/config i credentials
https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-files.html

vagrant up; vagrant status; vagrant ssh; vagrant reload -provision
docker info; docker version

# Install terraform
sudo apt-get update && sudo apt-get install -y gnupg software-properties-common curl

curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -

sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"

sudo apt-get update && sudo apt-get install terraform

terraform -version
terraform -help

## Install autocomplete (optional)
touch ~/.bashrc
terraform -install-autocomplete

## Install Docker if needed
https://docs.docker.com/engine/install/ubuntu/
More in the helper command

## NGINX with docker on linux
Jesli problem to:
https://learn.hashicorp.com/tutorials/terraform/install-cli?in=terraform/aws-get-started

mkdir tf-docker-nginx
cd tf-docker-nginx

main.tf with content as in my sample

terraform init
terraform plan -out plan
terraform apply "plan"

docker ps
localhost:8000

terraform state show docker_container.nginx

terraform destroy


# AWS Samples

## Install AWS CLI
https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html

curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install

aws --version

## Terraform config and AWS credentials 
export AWS_ACCESS_KEY_ID="AK"
export AWS_SECRET_ACCESS_KEY="Ip"
export AWS_DEFAULT_REGION="eu-west-1"


## Tworzenie EC2
https://learn.hashicorp.com/tutorials/terraform/aws-build?in=terraform/aws-get-started

mkdir
touch main.tf

### Inspect State
terraform state list
terraform pull
terraform show

## Dodac plik z security grupa
touch security-group.tf

## Utworzyc security grupe bioraca nazwe z pliku ze zmiennymi

## Change sth in EC2 - np. dodajcie kod, który przypnie wersję providera i Waszej wersji terraforma
## Destroy

# EC2 z kluczem SSH
ssh-keygen -o -a 100 -t ed25519 -f ~/.ssh/id_ed25519 -C aws_instance
touch key-pair.tf
data "local_file" "ssh_key" wskazujący na ~/.ssh/id_ed25519
resource "aws_key_pair" "this", puplic key wskazujacy na file

# Dodać output z ip adresem
output "public_ip_address" {
  value = aws_instance.this.public_ip
}

# Wyswietlic output
terraform output

# Sprawdz połączenie - ping, telnet, ssh?
ssh ubuntu@3.122.127.34 -i /home/vagrant/.ssh/id_ed25519

# 02 - Uruchomić moduł VPC z korzystając z module registry, z definicją providera w osobnym pliku
https://registry.terraform.io/modules/terraform-aws-modules/vpc/aws/latest

# 03 - Utworzyc bez powtarzania kodu 3 instancje EC2 (count)

# 03b - Utworzyc bez powtarzania kodu 3 instancje EC2 (for_each)

# Destroy everything

# 04 - Killer - EC2 module
Utworzyć instancje EC2, które będą tworzone za pomocą modułu, a obraz ubuntu będzie dynamicznie pobierany i filtrowany, tak żeby wykorzystywany był najnowszy obraz Ubuntu Canonical. Każda instancja ma być podłączona do niedefaultowego i utworzonego VPC, w osobnych subnetach publicznych i osobnych security grupach.
Zmienne trzymane w pliku variables, output adresu IP

subnet_id = module.vpc.public_subnets[0]

# Jak za dużo czasu to pokazać (przygot przyklady):
Funkcje formatujące
Count
For_each
Backend configuration sample
Auto-vpc
Ciekawe toole z githuba: (terrafognita, graph beautifier)
https://github.com/shuaibiyy/awesome-terraform




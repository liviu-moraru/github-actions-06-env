# Sectiunea 6. Using Environment Variables & Secrets

## Conexiune la MongoDB in cloud

- Am creat cont in cloud-ul MongoDb (user: liviu.moraru@gmail.com)
- 
User: liviu
Password: 5yiLcrf6LWJtPNrn
MONGODB_CLUSTER_ADDRESS: cluster0.iivyk6h.mongodb.net

Stringul de conectare: mongodb+srv://liviu:<password>@cluster0.iivyk6h.mongodb.net/?retryWrites=true&w=majority

## Variabilele de environment in workflow

- Pot fi definite la nivel de step, job sau workflow prin atributul env
- Accesate in workflow fie direct (in bash ca $VAR) sau prin context object ${{ env.VAR }}


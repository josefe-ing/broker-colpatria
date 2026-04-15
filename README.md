# BrokerAPP — Constructora Colpatria
## Demo de plataforma de micro-brokers VIS

### Deploy en DigitalOcean App Platform (Opción recomendada)

**Vía GitHub (más fácil):**

1. Crea un repo en GitHub:
```bash
cd broker-colpatria
git init
git add .
git commit -m "BrokerAPP Colpatria demo v1"
git branch -M main
git remote add origin git@github.com:tu-usuario/broker-colpatria.git
git push -u origin main
```

2. En DigitalOcean:
   - Ve a **App Platform** → **Create App**
   - Conecta tu repo de GitHub
   - Selecciona **Static Site**
   - Deploy → listo, te da URL tipo `broker-colpatria-xxxxx.ondigitalocean.app`

**Vía doctl CLI (si ya lo tienes configurado):**

```bash
# Desde la carpeta del proyecto
doctl apps create --spec .do/app.yaml
```

---

### Deploy en DO Spaces + CDN (alternativa)

```bash
# Crear bucket
doctl spaces create broker-colpatria --region nyc3

# Subir archivo
s3cmd put index.html s3://broker-colpatria/ \
  --acl-public \
  --mime-type="text/html" \
  --add-header="Cache-Control:max-age=3600"

# URL: https://broker-colpatria.nyc3.digitaloceanspaces.com/index.html
# O con CDN: https://broker-colpatria.nyc3.cdn.digitaloceanspaces.com/index.html
```

---

### Deploy en Droplet existente (si ya tienes uno)

```bash
# Copia el archivo al droplet
scp index.html root@TU_IP:/var/www/html/broker/index.html

# Si usas nginx, agrega un server block:
# server {
#     listen 80;
#     server_name broker.tudominio.com;
#     root /var/www/html/broker;
#     index index.html;
# }
```

---

### Dominio personalizado

Una vez deployado, puedes agregar un dominio personalizado:
- `broker.algorithm-ia.com`
- `broker.colpatria-demo.com`
- O el subdominio que prefieras

En DO App Platform: Settings → Domains → Add Domain → configura el CNAME.

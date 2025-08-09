## Paso 0: Vinculación
gcloud init

## Paso 1: Creación del repositorio
gcloud artifacts repositories create repo-mlops12-sesion3-frontend-streamlit --repository-format docker --project mlops12-carlos-sanchez --location us-central1

gcloud artifacts repositories create repo-mlops12-sesion3-frontend-streamlit-regresion --repository-format docker --project mlops12-carlos-sanchez --location us-central1

## Paso automatizacion

git init
git add . 
git commit -m "Proyecto de automatizaciòn de despiegue con GCR"
git branch -M main
git remote add origin https://github.com/The-carlos/mlops12-deploy-gcr-streamlit-regresion.git
git push -u origin main

## Paso 2: Crear la imagen de mi APLICACION y subir al repositorio
gcloud builds submit --config=cloudbuild.yaml --project mlops12-carlos-sanchez

## Paso 3: Comando para despliegue o ejecución de la imagen en el repositorio
gcloud run services replace service.yaml --region us-central1 --project mlops12-carlos-sanchez

## Paso 4: OPCIONAL, Dar permisos de acceso a mi APLICACION. ESTO SE EJECUTA UNA SOLA VEZ
gcloud run services set-iam-policy ervicio-streamlit-carlos-sanchez gcr-service-policy.yaml --region us-central1 --project mlops12-carlos-sanchez
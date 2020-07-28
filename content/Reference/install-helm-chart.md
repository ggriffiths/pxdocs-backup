---
title: PX-Backup installation Helm chart reference
description: Look up API endpoints and parameters.
keywords: 
weight: 11
disableprevnext: true
scrollspy-container: false
type: common-landing
# series: backup
---

The following table lists the configurable parameters of the PX-Backup Helm chart and their default values.

Parameter | Description | Default
--- | --- | ---
`persistentStorage` | Persistent storage for all px-central components | `""`
`persistentStorage.enabled` | Enable persistent storage | `false`
`persistentStorage.storageClassName` | Provide storage class name which exists | `""`
`storkRequired` | Scheduler name as stork | `false`
`pxcentralDBPassword` | PX-Central cluster store mysql database password | `Password1`
`oidc` | Enable OIDC for PX-Central and PX-backup for RBAC | `""`
`oidc.centralOIDC` | PX-Central OIDC | `""`
`oidc.centralOIDC.enabled` | PX-Central OIDC | `true`
`oidc.centralOIDC.defaultUsername` | PX-Central OIDC username | `admin`
`oidc.centralOIDC.defaultPassword` | PX-Central OIDC admin user password | `admin`
`oidc.centralOIDC.defaultEmail` | PX-Central OIDC admin user email | `admin@portworx.com`
`oidc.centralOIDC.keyCloakBackendUserName` | Keycloak backend store username | `keycloak`
`oidc.centralOIDC.keyCloakBackendPassword` | Keycloak backend store password | `keycloak`
`oidc.centralOIDC.clientId` | PX-Central OIDC client id | `pxcentral`
`oidc.centralOIDC.clientSecret` | PX-Central OIDC client secret | `dummy`
`oidc.externalOIDC` | Enable external OIDC provider | `""`
`oidc.externalOIDC.enabled` | Enabled external OIDC provider | `false`
`oidc.externalOIDC.clientID` | External OIDC client ID | default `""`
`oidc.externalOIDC.clientSecret` | External OIDC client secret | `""`
`oidc.externalOIDC.endpoint` | External OIDC endpoint | `""`
`images` | PX-Backup deployment images | `""`
`pxbackup` | Enable PX-Backup | `""`
`pxbackup.enabled` | Enabled PX-Backup | `true`
`pxbackup.orgName` | PX-Backup organization name | `default`
`securityContext` | Security context for the pod | `{runAsUser: 1000, fsGroup: 1000, runAsNonRoot: true}`
`images.pullSecrets` | Image pull secrets | `docregistry-secret`
`images.pullPolicy` | Image pull policy | `Always`
`images.pxcentralApiServerImage.registry` | API server image registry | `docker.io`
`images.pxcentralApiServerImage.repo` | API server image repo | `portworx`
`images.pxcentralApiServerImage.imageName` | API server image name | `pxcentral-onprem-api`
`images.pxcentralApiServerImage.tag` | API server image tag | `1.0.4`
`images.pxcentralFrontendImage.registry` | PX-Central frontend image registry | `docker.io`
`images.pxcentralFrontendImage.repo` | PX-Central frontend image repo | `portworx`
`images.pxcentralFrontendImage.imageName` | PX-Central frontend image name | `pxcentral-onprem-ui-frontend`
`images.pxcentralFrontendImage.tag` | PX-Central frontend image tag | `1.1.2`
`images.pxcentralBackendImage.registry` | PX-Central backend image registry | `docker.io`
`images.pxcentralBackendImage.repo` | PX-Central backend image repo | `portworx`
`images.pxcentralBackendImage.imageName` | PX-Central backend image name | `pxcentral-onprem-ui-backend`
`images.pxcentralBackendImage.tag` | PX-Central backend image tag | `1.1.2`
`images.pxcentralMiddlewareImage.registry` | PX-Central middleware image registry | `docker.io`
`images.pxcentralMiddlewareImage.repo` | PX-Central middleware image repo | `portworx`
`images.pxcentralMiddlewareImage.imageName` | PX-Central middleware image name | `pxcentral-onprem-ui-lhbackend`
`images.pxcentralMiddlewareImage.tag`| PX-Central middleware image tag | `1.1.2`
`images.pxBackupImage.registry` | PX-Backup image registry | `docker.io`
`images.pxBackupImage.repo` | PX-Backup image repo | `portworx`
`images.pxBackupImage.imageName` | PX-Backup image name | `px-backup`
`images.pxBackupImage.tag` | PX-Backup image tag | `1.0.2`
`images.postInstallSetupImage.registry` | PX-Backup post install setup image registry | `docker.io`
`images.postInstallSetupImage.repo` | PX-Backup post install setup image repo | `portworx`
`images.postInstallSetupImage.imageName` | PX-Backup post install setup image name | `pxcentral-onprem-post-setup`
`images.postInstallSetupImage.tag` | PX-Backup post install setup image tag | `1.0.4`
`images.etcdImage.registry` | PX-Backup etcd image registry | `docker.io`
`images.etcdImage.repo` | PX-Backup etcd image repo | `bitnami`
`images.etcdImage.imageName` | PX-Backup etcd image name | `etcd`
`images.etcdImage.tag` | PX-Backup etcd image tag | `3.4.7-debian-10-r14`
`images.keycloakBackendImage.registry` | PX-Backup keycloak backend image registry | `docker.io`
`images.keycloakBackendImage.repo` | PX-Backup keycloak backend image repo | `bitnami`
`images.keycloakBackendImage.imageName` | PX-Backup keycloak backend image name | `postgresql`
`images.keycloakBackendImage.tag` | PX-Backup keycloak backend image tag | `11.7.0-debian-10-r9`
`images.keycloakFrontendImage.registry` | PX-Backup keycloak frontend image registry | `docker.io`
`images.keycloakFrontendImage.repo` | PX-Backup keycloak frontend image repo | `jboss`
`images.keycloakFrontendImage.imageName` | PX-Backup keycloak frontend image name | `keycloak`
`images.keycloakFrontendImage.tag` | PX-Backup keycloak frontend image tag | `9.0.2`
`images.keycloakLoginThemeImage.registry` | PX-Backup keycloak login theme image registry | `docker.io`
`images.keycloakLoginThemeImage.repo` | PX-Backup keycloak login theme image repo | `portworx`
`images.keycloakLoginThemeImage.imageName` | PX-Backup keycloak login theme image name | `keycloak-login-theme`
`images.keycloakLoginThemeImage.tag` | PX-Backup keycloak login theme image tag | `1.0.2`
`images.keycloakInitContainerImage.registry` | PX-Backup keycloak init container image registry | `docker.io`
`images.keycloakInitContainerImage.repo` | PX-Backup keycloak init container image repo | `library`
`images.keycloakInitContainerImage.imageName` | PX-Backup keycloak init container image name | `busybox`
`images.keycloakInitContainerImage.tag` | PX-Backup keycloak init container image tag | `1.31`
`images.mysqlImage.registry` | PX-Central cluster store mysql image registry | `docker.io`
`images.mysqlImage.repo` | PX-Central cluster store mysql image repo | `library`
`images.mysqlImage.imageName` | PX-Central cluster store mysql image name | `mysql`
`images.mysqlImage.tag` | PX-Central cluster store mysql image tag | `5.7.22`
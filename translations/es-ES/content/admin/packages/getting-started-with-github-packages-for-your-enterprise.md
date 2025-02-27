---
title: Iniciar con GitHub Packages para tu empresa
shortTitle: Comenzar con los Paquetes de GitHub
intro: 'Puedes comenzar a utilizar el {% data variables.product.prodname_registry %} en {% data variables.product.product_location %} si habilitas esta característica, configurando un almacenamiento de terceros, configurando los ecosistemas que quieras que sea compatibles y actualizando tu certificado TLS.'
redirect_from:
  - /enterprise/admin/packages/enabling-github-packages-for-your-enterprise
  - /admin/packages/enabling-github-packages-for-your-enterprise
versions:
  ghes: '*'
type: how_to
topics:
  - Enterprise
  - Packages
---


{% data reusables.package_registry.packages-cluster-support %}

## Paso 1: Verifica si el {% data variables.product.prodname_registry %} está disponible para tu empresa

El {% data variables.product.prodname_registry %} está disponible para {% data variables.product.prodname_ghe_server %} 3.0 o superior. Si estás utilizando una versión más antigua de {% data variables.product.prodname_ghe_server %}, tendrás que mejorarla para utilizar el {% data variables.product.prodname_registry %}. Para obtener más información sobre cómo mejorar tu instancia de {% data variables.product.prodname_ghe_server %}, consulta la sección "[Acerca de las mejoras a los lanzamientos nuevos](/admin/overview/about-upgrades-to-new-releases)".
## Paso 2: Habilita el {% data variables.product.prodname_registry %} y configura el almacenamiento externo

{% data variables.product.prodname_registry %} en {% data variables.product.prodname_ghe_server %} utiliza almacenamiento externo de blobs para almacenar tus paquetes.

Después de habilitar el {% data variables.product.prodname_registry %} para {% data variables.product.product_location %}, necesitarás preparar tu bucket de almacenamiento de terceros. La cantidad de almacenamiento que requieras dependerá de tu uso del {% data variables.product.prodname_registry %}, y los lineamientos de configuración podrán variar dependiendo del proveedor de almacenamiento.

Proveedores de almacenamiento externo compatibles
- Amazon Web Services (AWS) S3 {% ifversion ghes %}
- Azure Blob Storage {% endif %}
- MinIO

Para habilitar el {% data variables.product.prodname_registry %} y configurar el almacenamiento de terceros, consulta:
  - "[Habilitar GitHub Packages con AWS](/admin/packages/enabling-github-packages-with-aws)"{% ifversion ghes %}
  - "[Habilitar GitHub Packages con Azure Blob Storage](/admin/packages/enabling-github-packages-with-azure-blob-storage)"{% endif %}
  - "[Habilitar GitHub Packages con MinIO](/admin/packages/enabling-github-packages-with-minio)"

## Paso 3: Especifica los ecosistemas de paquetes que serán compatibles con tu instancia

Elige qué ecosistemas de paquetes te gustaría habilitar, inhabilitar o configurar como de solo lectura en tu {% data variables.product.product_location %}. Available options are {% ifversion ghes > 3.4 %}{% data variables.product.prodname_container_registry %}, {% endif %}Docker, RubyGems, npm, Apache Maven, Gradle, or NuGet.  Para obtener más información, consulta la sección "[Configurar la compatibilidad de ecosistemas de paquetes para tu empresa](/enterprise/admin/packages/configuring-package-ecosystem-support-for-your-enterprise)".

## Paso 4: De ser necesario, asegúrate de que tienes un certificado de TLS para la URL de hospedaje de tu paquete

If subdomain isolation is enabled for {% data variables.product.product_location %}, you will need to create and upload a TLS certificate that allows the package host URL for each ecosystem you want to use, such as `{% data reusables.package_registry.container-registry-hostname %}`. Asegúrate de que cada URL de host de paquete incluya `https://`.

  Puedes crear el certificado manualmente, o puedes utilizar _Let's Encrypt_. Si ya utilizas _Let's Encrypt_, debes solicitar un certificado TLS nuevo después de habilitar el {% data variables.product.prodname_registry %}. Para obtener más información acerca de las URL del host de los paquetes, consulta "[Habilitar el aislamiento de subdominios](/enterprise/admin/configuration/enabling-subdomain-isolation)". Para obtener más información sobre cómo cargar certificados TLS a {% data variables.product.product_name %}, consulta la sección "[Configurar el TLS](/enterprise/admin/configuration/configuring-tls)".

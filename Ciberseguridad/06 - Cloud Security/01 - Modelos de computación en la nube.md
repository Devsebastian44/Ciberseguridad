## Modelos de Servicio en la Nube

### IaaS (Infrastructure as a Service)

- **Definición**: Provisión de recursos de infraestructura virtualizada (servidores, almacenamiento, redes)
- **Control**: El usuario gestiona SO, aplicaciones, datos y configuraciones
- **Proveedor gestiona**: Hardware físico, virtualización, redes físicas
- **Ejemplos**: AWS EC2, Azure Virtual Machines, Google Compute Engine
- **Caso de uso**: Migración lift-and-shift, entornos de desarrollo/pruebas

### PaaS (Platform as a Service)

- **Definición**: Plataforma completa para desarrollar, ejecutar y gestionar aplicaciones
- **Control**: El usuario gestiona aplicaciones y datos
- **Proveedor gestiona**: SO, middleware, runtime, infraestructura
- **Ejemplos**: AWS Elastic Beanstalk, Azure App Service, Google App Engine
- **Caso de uso**: Desarrollo de aplicaciones sin gestionar infraestructura

### SaaS (Software as a Service)

- **Definición**: Aplicaciones completas entregadas por internet
- **Control**: El usuario solo consume el servicio
- **Proveedor gestiona**: Todo (aplicación, datos, runtime, SO, infraestructura)
- **Ejemplos**: Microsoft 365, Salesforce, Google Workspace
- **Caso de uso**: Productividad, CRM, correo electrónico

## Modelos de Implementación

### Nube Pública

- Infraestructura compartida entre múltiples organizaciones
- Gestionada por proveedor externo
- Mayor escalabilidad y menor costo inicial

### Nube Privada

- Infraestructura dedicada a una sola organización
- Mayor control y personalización
- Puede estar on-premises o gestionada por terceros

### Nube Híbrida

- Combinación de nube pública y privada
- Permite mover cargas de trabajo entre ambas
- Balance entre control y flexibilidad

### Multi-Cloud

- Uso de múltiples proveedores de nube
- Evita dependencia de un solo proveedor
- Optimización de costos y servicios específicos

## Modelo de Responsabilidad Compartida

**Importante**: La seguridad en la nube es una responsabilidad compartida entre proveedor y cliente

- **Proveedor**: Seguridad "DE" la nube (infraestructura física, red, hipervisor)
- **Cliente**: Seguridad "EN" la nube (datos, aplicaciones, identidades, configuraciones)
- La responsabilidad del cliente aumenta de SaaS → PaaS → IaaS
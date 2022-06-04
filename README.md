# riscv-cluster
Información sobre cluster RISCV64, utilizado para proyectos como Slackware y CBL-Mariner

## Servicios de Cluster

### Sccache

Se provee un acceso privado al cluster de compilación de [sccache](https://github.com/mozilla/sccache) de Mozilla, el cual funciona de manera similar a ccache, distcc o icecc, pero con soporte para almacenamiento en nubes como la de Azure, y con capacidad para compilar aplicaciones en Rust.

TODO:
- [x] Lograr compilación en RISCV64: La dependencia de ring estaba presentando problemas para compilar en riscv64, por lo cual se siguen instrucciones en [bug #1419 de Ring](https://github.com/briansmith/ring/issues/1419), se ejecuta ``build`` y ``build --tests`` con todo éxito, por lo que se procede a realizar [parche y pull request](https://github.com/briansmith/ring/pull/1500) el cual está esperando por ser integrado. Si necesita compilar sccache o algún otro software que utilice ring como dependencia, puede utilizar el repositorio de @fede2cr de ring para realizar una compilación exitosa, mientras esperamos a que se integre el pull request.
- [x] Realizar pruebas básicas de sccache con código de Rust y de C/C++. Se realiza la compilación de (coreutils en rust)[https://github.com/uutils/coreutils], con todo éxito. Luego se eliminó el código y se ejecutó de nuevo, podiendo el sistema encontrar los objetos del caché según se espera.
- [ ] Generar documentación sobre uso distribuido de sccache. Debe incluir: a) poder crear varios servicios en una misma red, para poder acomodar a diferentes distribuciones como Slackware y CBL-Mariner. b) información para conectar con nube de Azure. c) uso básico para desarrolladores.
- [ ] Compartir documentación de sccache con el proyecto de Cluster RISCV64 de PLCT Lab.

### Runners para Github

Los runners de Github, son componentes que permiten ejecutar código del CI/CD de Github, en una computadora externa a la plataforma de Github. Actualmente esto es necesario, ya que no existen runners en Github para la plataforma de RISCV64, por lo que esto permitiría ejecutar CI/CD en hardware de este cluster.

Si necesita acceso a self-hosted Runners de Github, consulte con @fede2cr para recibir acceso, dependiendo de la naturaleza del proyecto a ejecutar.

TODO:

- [ ] Actualmente se ha tratado de correr el runner oficial de Github, sin embargo Dotnet (no corre en RISCV64)[https://github.com/dotnet/runtime/issues/36748], por lo cual se opta por buscar alternativas.
- [ ] Se está probando [gha-runner de Rust-lang](https://github.com/rust-lang/gha-runner). Este es un proyecto con advertencia de no usarse y sin soporte, sin embargo parece ser una alternativa mucho más rápida a esperar al equipo de Dotnet.

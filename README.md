# Repositorio Privado De Void Linux
---

## Como usar este repositorio

1. Edita el siguiente archivo:
```
sudo nano /etc/xbps.d/99-github.conf

```

2. Pega el siguiente contenido:

```
repository=https://raw.githubusercontent.com/mojamuto/my_void_templates/main/hostdir/binpkgs

```


>⚠️ Es importante que uses la URL de raw.githubusercontent.com, ya que XBPS necesita acceder directamente a los archivos binarios.

3. Sincroniza los Repositorios:

```
sudo xbps-install -S
```

4. Ya puedes instalar cualquier paquete que este en este repositorio:

```
sudo xbps-install nombre-del-paquete
```

---

# Añadir Paquetes Al Repositorio

* create a repository.
  1. xbps-rindex -a *.xbps
  2. xbps-install --repository=$PWD pkgname



Supongamos que tienes este repositorio local:
```
~/void-repo/hostdir/binpkgs/
```

Y dentro están los .xbps:
```
cd ~/void-repo/hostdir/binpkgs
xbps-rindex -a ./*.xbps
```
>Esto crea un archivo llamado x86_64-repodata necesario para poder añadir el repositorio github como repositorio de void linux.

## PASO 2

1. Generar una clave privada en formato PEM

Puedes generar una clave privada en formato PEM utilizando uno de los siguientes métodos:

Usando ssh-keygen:

```
ssh-keygen -t rsa -m PEM -f private.pem
```


2. Firmar los paquetes .xbps

Para firmar los paquetes individuales en tu repositorio, utiliza el siguiente comando:

```
xbps-rindex --privkey ~/.ssh/private.pem --sign-pkg --signedby "mojamuto" /home/carlos/Git/my_void_templates/hostdir/binpkgs/av1an-0.4.4_1.x86_64.xbps

```

Esto creará:

av1an-0.4.4_1.x86_64.xbps.sig

Luego, sube ese archivo .sig a tu repo (junto con el .xbps y el x86_64-repodata re-generado si hiciste cambios)

hay un script llamado firmar.sh para firmar todos los paquete a la vez



## PASO 3

1. Sube tus paquetes .xbps junto s x86_64-repodata a tu repositorio GitHub:

```
git add x86_64-repodata
git commit -m "Añadir índice de repositorio para xbps"
git push
```


3. Actualizar e instalar paquetes


🧪 Verificación

Si algo falla al instalar, puedes probar:
```
xbps-query -r / -L

```

✅ Opción 1: Crear la firma .sig para tus paquetes

🔐 Paso 1: Generar una clave privada en formato PEM

Puedes generar una clave privada en formato PEM utilizando uno de los siguientes métodos:

Usando ssh-keygen:

```
ssh-keygen -t rsa -m PEM -f private.pem
```


📦 Paso 3: Firmar los paquetes .xbps

Para firmar los paquetes individuales en tu repositorio, utiliza el siguiente comando:
```
xbps-rindex --privkey ~/.ssh/private.pem --sign-pkg --signedby "mojamuto" /home/carlos/Git/my_void_templates/hostdir/binpkgs/av1an-0.4.4_1.x86_64.xbps

```

Esto creará:

av1an-0.4.4_1.x86_64.xbps.sig

Luego, sube ese archivo .sig a tu repo (junto con el .xbps y el x86_64-repodata re-generado si hiciste cambios)

hay un script llamado firmar.sh para firmar todos los paquete a la vez

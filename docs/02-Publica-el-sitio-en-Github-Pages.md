1. Crea el directorio `.github` a nivel raíz del proyecto.

    ```BASH
    mkdir .github
    ```
    ![IMG-24](./assets/24.png)

2. Crea el directorio `workflows` dentro de `.github`.

    ```BASH
    mkdir .github/workflows
    ```
    ![IMG-25](./assets/25.png)

3. Crea el fichero `ci.yml` dentro de `workflows`.
    ```BASH
    touch .github/workflows/ci.yml
    ```
    ![IMG-26](./assets/26.png)

    Deberías poder ver la siguiente estructura en tu editor de código:

    ![IMG-27](./assets/27.png) 

4. Copia el siguiente código en el fichero `ci.yml` para automatizar la compilación y despliegue de tu sitio cada que hagas un `push`a github. 

    ```YAML
    name: ci 
    on:
        push:
            branches:
                - master 
                - main
    permissions:
        contents: write
    jobs:
        deploy:
            runs-on: ubuntu-latest
            steps:
                - uses: actions/checkout@v3
                - uses: actions/setup-python@v4
                  with:
                    python-version: 3.x
                - uses: actions/cache@v2
                  with:
                    key: ${{ github.ref }}
                    path: .cache
                - run: pip install mkdocs-material
                - run: pip install pillow cairosvg
                - run: mkdocs gh-deploy --force
    ```

5. Añade el contenido a los archivos que rastrea github con el siguiente comando:

    ```BASH
    git add -A
    ```

6. Realiza un commit del estado actual de tu sitio:

    ```BASH
    git commit -m "Añadiendo la configuración inicial para mkdocs"
    ```

7. Manda tu versión a github:

    ```BASH
    git push origin main
    ```

8. Dirigete al repositorio en Github

    ![IMG-28](./assets/28.png)

9. Da click en el apartado "settings".

    ![IMG-29](./assets/29.png)

10. En el menú lateral busca la opción "pages".

    ![IMG-30](./assets/30.png)

11. Ya en Github Pages en el apartado "Branch" selecciona la opción `gh-pages`.

    ![IMG-31](./assets/31.png)

    Una vez seleccionado de click en "Save".

    ![IMG-32](./assets/32.png)

12. Dirigite a "Actions"

    ![IMG-33](./assets/33.png)

13. Selecciona el workflow llamado "ci" situado en la barra del lateral izquierdo.
    
    ![IMG-34](./assets/34.png)

    Entra en la acción dando click en el título

    ![IMG-35](./assets/35.png)

    Da click en el job llamado "deploy"

    ![IMG-36](./assets/36.png)

    Despliega el paso "Run mkdocs gh-deploy --force"

    ![IMG-37](./assets/37.png)

    Note que en el paso final verá una nota informativa que le dirá la URL mediante la cual podrá acceder a su sitio. 



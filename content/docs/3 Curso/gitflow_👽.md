# Comandos avanzados para Github
---
- Resetear toda la rama (borra los cambios no guardados) `git reset`
- Ver los cambios creados `git log --oneline`
- Añadir los cambios a un repo (añade todo) `git add .`
- Crear un commit `git commit -m "<message>"`
- Subir el código `git push`
- Ver el estado de la rama `git status`
- Cambiar entre ramas `git checkout <rama>`
- Eliminar una rama (en caso de que nada funcionase) `git branch -D <rama>`
- Crear una rama y movernos a ella directamente `git checkout -b <rama>`
- Unir ramas->posicionarse en la rama que queremos mergear y hacer `git merge <rama>`
- Si queremos cambiar el nombre de un push que hayamos nombrado mal:
````cmd
git reset --soft HEAD~1
git add .
git commit -m "custom message"
git push -u -f origin master
````
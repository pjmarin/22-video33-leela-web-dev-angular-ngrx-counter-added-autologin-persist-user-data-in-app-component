En este video hemos agregado implementado la funcionalidad de autologin, para que cuando actualicemos la pagina, siga la informacion del usuario vigente, lo que seria una sesion.
Hemos guardado los datos del usuario en localstorage, lo cual no seria correcto del todo por motivos de seguridad, y la clave para persistir los datos es hacer los cambios en el
componente app.component.ts, es decir el componente general que contiene toda la aplicacion.
Aqui en el app.component.ts llamamos a this.store.dispatch(autoLogin()); en el ngOnInit()
La accion la hemos definido en public/src/app/auth/state/auth.actions.ts

export const AUTO_LOGIN_ACTION = '[auth page] auto login';

export const autoLogin = createAction(AUTO_LOGIN_ACTION);

En el archivo de effects public/src/app/auth/state/auth.effects.ts

llamamos en el effect login$ y en el effect signUp$ al metodo nuevo que definiremos en el service --> this.authService.setUserInLocalStorage(user);

y creamos un nuevo effect --> autoLogin$ = createEffect(

en el cual llamaremos a otro metodo nuevo que definiremos en el service --> this.authService.getUserFromLocalStorage(user); para persistir los datos en el app.component.ts, que es donde despachamos la accion de autologin
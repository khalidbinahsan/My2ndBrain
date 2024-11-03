Well, if you want to protect any of your routers that the user is not authenticated will redirect to the "/login" page you can use the vue-router global guard **beforeEach()** funciton. Here is the example
```js
const routes = [
	{
        path: '/login',
        component: Login,
        name: "Login"
    },
    {
        path: '/register',
        component: Register,
        name: "Register"
    },
    {
        path: '/user',
        component: User,
        name: 'User',
        meta: {requiresAuth: true},
        children: [
            {
                path: "",
                component: Dashboard,
                name: "Dashboard"
            },
        ]
    }
]

const router = createRouter({
    history: createWebHistory(),
    routes: routes
})
router.beforeEach((to, from, next) => {
    const requiresAuth = to.matched.some((record) => record.meta.requiresAuth)
    if(requiresAuth){
        next({name: "Login"})
    } else {
        next()
    }
})
export default router;
```

### Let's explain
As you can see the **beforeEach** triggering every route when is change. If you want to active any route the guard, just put the meta **requresAuth: true** 

if the **requresAuth** is true, it will redirect the user to the **login** page. After that you can make it's value false by checking the authentication.
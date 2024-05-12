We used the **Promise** in the function here [[Promise() object]] Here is the example, how use **async** & **await** instead of using **.then**

```js
async function course(){
  try{
    await enroll();
    await progress();
    const message = await getCertificate();
    console.log(message)
  } catch (error) {
    console.log(error)
  }
}
```
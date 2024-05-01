Here is the example of **new Promise()** object
``` js
const paymentSuccess = true
const marks = 80

function enroll(){
  console.log('Course enrollment is progress')
  const promise = new Promise((resolve, reject) => {
    setTimeout(() => {
      if(paymentSuccess){
        resolve()
      } else {
        reject('Payment failed')
      }
    }, 3000)
  })
  return promise
}

function progress(){
  console.log('Course on progress...')
  const promise = new Promise((resolve, reject) => {
    setTimeout(() => {
      if(marks >= 80){
        resolve()
      } else {
        reject('Sorry! you could no get enough marks to get the certificate')
      }
    }, 3000)
  })
  return promise
}

function getCertificate(){
  console.log('Preparing your certificate')
  const promise = new Promise((resolve) => {
    setTimeout(() => {
      resolve('Congrats! you get the certificate')
    }, 1000)
  })
  return promise
}

enroll()
.then(progress)
.then(getCertificate)
.then((value) => {
  console.log(value)
})
.catch((error) => {
console.log(error)
})
```
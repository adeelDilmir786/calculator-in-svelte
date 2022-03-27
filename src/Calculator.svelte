<script>
	import Keypad from './Keypad.svelte';

	let pin;
	$: view = pin ?pin:'0'

	function handleSubmit() {
    //    alert( view.test(/^(.*[+,/,*,-])?$/igm));
   const lastChar=view[view.length-1]
       if(view[0]==='+'||view[0]==='-'||view[0]==='*'||view[0]==='/'||lastChar==='+'||lastChar==='-'||lastChar==='/'||lastChar==='*')
       {
           alert("Invalid operation");
           return;
       }
       if(view.includes('++')||view.includes('--')||view.includes('//')||view.includes('**')
          ||view.includes('+-')||view.includes('+*')||view.includes('+/') 
          ||view.includes('-+')||view.includes('-*')||view.includes('-/') 
          ||view.includes('*+')||view.includes('*-')||view.includes('*/')
         )
       {
           alert("Invalid operation");
           return;
       } 
   
       let previousIndex='';
       let inputArray=[];

       for(let i=0 ; i< view.length;i++){
        
        if(view[i]==='*'||view[i]==='/'||view[i]==='+'||view[i]==='-'){

        if(previousIndex)
        {
          inputArray.push(parseInt( view.substring(previousIndex,i)))
          inputArray.push(view.substring(i,i+1))
          previousIndex=i+1;
          
        }else{

          inputArray.push(parseInt(view.substring(0,i))) 
          inputArray.push(view.substring(i,i+1))
          previousIndex=i+1;
 
        }          
    } 

    }
    inputArray.push(parseInt(view.substring(previousIndex,view.length)))


let operation='/';
let index;
console.log(inputArray);

    while(inputArray.length>1){


     if(operation==='/'||operation==='*')
     {
           const indexOfDivision= inputArray.indexOf('/');
           const indexOfMultiplication= inputArray.indexOf('*');
           let index;
           let ans;
           console.log('Div',indexOfDivision,'Mul',indexOfMultiplication)
           if(indexOfDivision===-1&&indexOfMultiplication===-1){
             operation='+';
             continue;
            }else if(indexOfDivision===-1){
             
             ans=multiplication(inputArray[indexOfMultiplication-1],inputArray[indexOfMultiplication+1]);
             index=indexOfMultiplication;
             console.log('1*',ans)
            }else if(indexOfMultiplication===-1){              
             ans=division(inputArray[indexOfDivision-1],inputArray[indexOfDivision+1]);
             console.log('2/',ans)
             index=indexOfDivision;
            }else if(indexOfDivision<indexOfMultiplication){
                ans=division(inputArray[indexOfDivision-1],inputArray[indexOfDivision+1]);
                index=indexOfDivision;
                console.log('3/',ans)
            }else {
                ans=multiplication(inputArray[indexOfMultiplication-1],inputArray[indexOfMultiplication+1]);
                index=indexOfMultiplication;
                console.log('4*',ans)
            }
            inputArray.splice(index-1,3,ans)
            console.log(inputArray)

     }else{
           const indexOfSum= inputArray.indexOf('+');
           const indexOfSub= inputArray.indexOf('-');
           let index;
           let ans;
           if(indexOfSum===-1&&indexOfSub===-1){
             operation='+';
             continue;
            }else if(indexOfSum===-1){
             
             ans=sub(inputArray[indexOfSub-1],inputArray[indexOfSub+1]);
             index=indexOfSub;

            }else if(indexOfSub===-1){
             ans=sum(inputArray[indexOfSum-1],inputArray[indexOfSum+1]);
             index=indexOfSum;
            }else if(indexOfSum<indexOfSub){
                ans=sum(inputArray[indexOfSum-1],inputArray[indexOfSum+1]);
                index=indexOfSum;
            }else {
                ans=sub(inputArray[indexOfSub-1],inputArray[indexOfSub+1]);
                index=indexOfSub;
            }
            inputArray.splice(index-1,3,ans)   
            console.log(inputArray)
     }

                
         
    }
        // console.log(view);
        // console.log(eval(pin))
        console.log(inputArray)
        view =inputArray[0];
        pin=inputArray[0];
        // view=eval(view);
		// pin=eval(view);
        // alert(`submitted ${pin}`);
	}

const multiplication=(a,b)=>a*b;
const division=(a,b)=>a/b;
const sum=(a,b)=>a+b;
const sub=(a,b)=>a-b;

</script>

<div>
<h1 style="color: {pin ? '#333' : '#ccc'}">{view}</h1>

<Keypad bind:value={pin} on:submit={handleSubmit}/>
</div>

<style>
h1{
height: 40px;
border: 1px solid grey;
width: 336px;
margin: 0px auto;
margin-bottom: 10px;
display: flex;
justify-content: flex-end;
padding: 5px;
border-radius: 5px;
}
</style>
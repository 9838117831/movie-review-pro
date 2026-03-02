# movie-review-pro
<button onclick="toggleTheme()">🌙 Toggle Theme</button>
body.dark{
background:#121212;
color:white;
}

body.dark section{
background:#1e1e1e;
}

body.dark .review{
background:#2a2a2a;
}
window.toggleTheme = function(){
document.body.classList.toggle("dark");
}
async function loadReviews(){

const querySnapshot = await getDocs(collection(db,"reviews"));
reviews.innerHTML="";
let totalRating = 0;
let count = 0;

querySnapshot.forEach(docSnap=>{
const data = docSnap.data();
totalRating += parseInt(data.rating);
count++;

reviews.innerHTML += `
<div class="review">
<img src="${data.poster}" width="100">
<div>
<h3>${data.movie}</h3>
<p>${data.review}</p>
<p>${data.rating} ⭐</p>
<button onclick="likeReview('${docSnap.id}', ${data.likes || 0})">
❤️ ${data.likes || 0}
</button>
</div>
</div>
`;
});

if(count > 0){
document.getElementById("avgRating").innerText =
"Average Rating: " + (totalRating/count).toFixed(1);
}
}
<h3 id="avgRating"></h3>
import { updateDoc } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-firestore.js";
window.likeReview = async function(id, currentLikes){

await updateDoc(doc(db,"reviews",id),{
likes: currentLikes + 1
});

loadReviews();
}
await addDoc(collection(db,"reviews"),{
movie,review,rating,poster,
likes:0,
comments:[]
});
<input placeholder="Add comment"
onkeydown="if(event.key==='Enter') addComment('${docSnap.id}', this.value)">
window.addComment = async function(id, comment){

const reviewRef = doc(db,"reviews",id);
const snapshot = await getDoc(reviewRef);
let data = snapshot.data();

data.comments.push(comment);

await updateDoc(reviewRef,{
comments: data.comments
});
loadReviews();
}
import { getDoc } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-firestore.js";
await addDoc(collection(db,"users"),{
email: email.value,
role: "user"
});
role: "admin"
@media(max-width:768px){

.review{
flex-direction:column;
}

header{
flex-direction:column;
gap:10px;
}

section{
margin:10px;
}
}

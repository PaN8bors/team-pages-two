<template>
	<div class="page-wrapper">
		<div class="compRow">
			<div class="compColumn-left">
				<div class="blobHolder">
					<div class="frame">
						<img class="pic" src="..\assets\blue-blob.png" />
					<div v-if="member.wasApprentice" class="badge"><img class="badge-image" src="..\assets\AppBadge.png" /></div>

					</div>
				</div>
			</div>
			<div class="compColumn-right">
				<div class="details">
					<h1 class="detailsFullName">{{ member.firstName }} {{ member.lastName }}</h1>
					<h2 v-if="member.pronouns != null" class="pronouns">({{ member.pronouns }})</h2>
					<h3 class="detailsTitle">{{ member.title }}</h3>
					<h6 class="startYear">{{ member.firstName }} joined SnapIT in {{ member.startYear }}.</h6>
					<h6 v-if="member.jobLikes != 'Did not answer.'" class="jobLikes">{{ member.jobLikes }}</h6>
				</div>
			</div>
		</div>
		<div class="lowerInfo">
			<div v-if="member.interests != 'Did not answer.'" class="interests">
				<h1 class="hobby">Hobbies and Interests</h1>
				<h5 class="hobbyData">{{ member.interests }}</h5>
			</div>
		</div>
		<div class="icons">
			<div v-if="member.linkedin != null">
				<a :href="'https://www.linkedin.com/in/' + member.linkedin">
				<img class="socialLink" src="..\assets\LinkedIn.webp"> </a>
			</div>
			<div v-if="member.github != null">
				<a :href="'https://github.com/' + member.github">
				<img class="socialLink" src="..\assets\GitHub.webp"> </a>
			</div>
			<div v-if="member.instagram != null">
				<a :href="'https://www.instagram.com/' + member.instagram">
				<img class="socialLink" src="..\assets\Insta.webp"> </a>
			</div>
			<div v-if="member.youtube != null">
				<a :href="'https://www.youtube.com/' + member.youtube">
				<img class="socialLink" src="..\assets\YouTube.webp"> </a>
			</div>
			<div v-if="member.personal != null">
				<a :href="member.personal">
				<img class="socialLink" src="..\assets\Link.webp"> </a>
			</div>
        </div>
	</div>
</template>

<script>
import { UserService } from "@/services/UserServices";

export default {
	name: "DetailsComponent",

	data: function() {
		return {
			loading: false,
			member: {},
			errorMessage: null
		};
	},

	created: async function() {
		let memberId = this.$route.params.memberId;

		try {
			this.loading = true;
			let response = await UserService.getMembers(memberId);
			console.log(response.data)
			this.loading = false;
			console.log(response.data);
			this.member = response.data;
		} catch (error) {
			this.loading = false;
			this.errorMessage = error;
		}
	},
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins&display=swap");


.compRow {
	display: flex;
	flex-direction: row;
	flex-wrap: wrap;
	width: 100%;
	align-items: flex-start;
}

.compColumn-left {
	display: flex;
	flex-direction: column;
	flex-basis: 100%;
	flex: 1;
    margin-left: 7%;
}

.compColumn-right {
	display: flex;
	flex-direction: column;
	flex-basis: 100%;
	flex: 1;
}

.blobHolder {
	display: flex;
	min-height: 500px;
	width: auto;
	margin-top: 50px;
	padding-left: 0%;
	padding-right: 0%;
}

.frame {
	position: relative;
	width: 600px;
	height: 550px;
	background-image: url(@/assets/sudheer.webp);
	background-repeat: no-repeat;
	background-position: left 100px top 40px;
	background-size: 85%;
}

.pic {
	position: absolute;
	left: 0;
	top: 0;
	right: 0;
	bottom: 0;
	display: block;
	margin: auto;
}

.badge {
	position: absolute;
	left: 370px;
	top: 390px;
	right: 0;
	bottom: 0;
	/* height: auto;
	width: 20px; */
	/* margin-top: -23%;
	padding-left: 68%;
	z-index: 1; */
}

.badge-image {
    height: auto;
	width: 200px;
}

.details {
	width: 75%;
	margin-right: 10%;
	margin-top: 175px;
	align-content: top;
	justify-content: left;
	padding-left: 18%;
}

.detailsFullName {
	font-size: 35px;
	font-weight: 600;
	font-style: normal;
	font-family: poppins;
	color: #0679be;
	line-height: 27px;
	margin-bottom: 10px;
	margin-top: 0px;
}

.interests {
	display: flex;
	flex-direction: column;
	color: black;
	font-family: poppins, sans-serif;
	width: 100%;
	margin-top: 30px;
	justify-content: center;
}

.lowerInfo {
	display: flexbox;
	flex-direction: column;
	justify-content: center;
	width: 100%;
}

.pronouns {
	font-size: 24px;
	font-family: poppins;
	font-weight: 600;
	line-height: 28px;
	margin-top: 0px;
	padding-bottom: 5px;
}

.detailsTitle {
	font-weight: 600;
	font-size: 18px;
	line-height: 27px;
	font-family: poppins;
	margin-bottom: 0px;
	color: gray;
}

.startYear {
	font-family: Poppins;
	font-weight: 600;
	font-size: 17px;
	line-height: 23px;
	color: gray;
	margin-top: 5px;
	margin-bottom: 0px;
}

.jobLikes {
	font-family: open-sans;
	font-weight: 400;
	font-size: 17px;
	font-stretch: 15%;
	line-height: 26px;
	color: #111111;
	margin-top: 25px;
	padding-right: 20%;
	justify-content: left;
}

.hobby {
	padding-left: 15%;
	width: 70%;
	font-family: poppins;
	font-weight: 600;
	font-size: 18px;
	line-height: 27px;
	color: #1b1b1b;
	text-align: center;
	margin-bottom: 0px;
}

.hobbyData {
	padding-left: 15%;
	width: 70%;
	font-family: open-sans;
	font-weight: 400;
	font-size: 17px;
	line-height: 26px;
	font-stretch: 15%;
	color: #111111;
	margin-top: 20px;
	margin-bottom: 0px;
	text-align: center;
}

.icons {
	display: flex;
	flex-direction: row;
	height: auto;
	width: 40%;
	padding-left: 30%;
	padding-bottom: 50px;
	justify-content: center;
	margin-top: 30px;
}

.socialLink {
    height: auto;
    width: 50px;
    padding-left: 15px;
    padding-right: 15px;
}
</style>

<template>
	<div id="app" class="container-fluid">
		<h1>Animações</h1>
		<hr>
		<b-button variant="primary" class="mb-4" 
		@click="exibir = !exibir">Mostrar Mensagem</b-button>
		<!-- <transition
		enter-active-class="animated bounce"
		leave-active-class="animated shake" appear>
			<b-alert variant="info" show v-if="exibir"> {{msg}}</b-alert>
		</transition>
		
		<transition name = "slide" type="animation" appear>
			<b-alert variant="info" show v-if="exibir"> {{msg}}</b-alert>
		</transition>
		<hr>
		<b-select v-model="tipoAnimacao" class="mb-4">
			<option value="fade">Fade</option>
			<option value="slide">Slide</option>
		</b-select> -->

		<!-- <transition :name="tipoAnimacao" mode="out-in" >
			<b-alert variant="info" show v-if="exibir" key="info"> {{msg}}</b-alert>
			<b-alert variant="warning" show v-else key="warn"> {{msg}}</b-alert>
		</transition>

		<hr>
		<button @click="exibir2 = !exibir2"> Alternar </button>
		<transition
		:css="false"
			@before-enter="beforeEnter"
			@enter="enter"

			@before-leave="beforeLeave"
			@leave="leave">
			<div v-if="exibir2" class="caixa"> </div>
		</transition>

		<hr>
		<div class="mb-4">
			<b-button variant="primary" class="mr-2"
			@click="componenteSelecionado = 'AlertaInfo'">Info</b-button>
			<b-button variant="secundary"
			@click="componenteSelecionado = 'AlertaAdvertencia'">Advertência</b-button>

		</div>
		<transition name="fade" mode="out-in">

		<component :is="componenteSelecionado"></component>
		</transition> -->
	
		<hr>

		<b-list-group v-for="aluno in alunos" :key="aluno">
		<b-list-group-item>{{aluno}}</b-list-group-item>

		</b-list-group>
	
	
	</div>
</template>

<script>
import AlertaAdvertencia from './AlertaAdvertencia.vue'
import AlertaInfo from './AlertaInfo.vue'
export default {
	components:{AlertaAdvertencia, AlertaInfo},
	data(){	
		return{
			alunos:['Robertpo', 'Julia', 'Teresa', 'Paulo'],
			msg: "Esta é a mensagem",
			exibir: false,
			exibir2: true,
			tipoAnimacao: 'fade',
			larguraBase: 0,
			componenteSelecionado: 'AlertaInfo',
		}
	}, 

	methods:{
		beforeEnter(el){
			this.larguraBase = 0
			el.style.width = `${this.larguraBase}px`
		},

		enter(el, done){
			let rodada = 1
			const temporizador = setInterval(()=>{
				const novaLargura = this.larguraBase + rodada * 10
				el.style.width = `${novaLargura}px`
				rodada++
				if(rodada > 30){
					clearInterval(temporizador)
					done()
				}
			}, 20)
			
		},

		beforeLeave(el){
			
			this.larguraBase = 300
			el.style.width = `${this.larguraBase}px`
		},

		leave(el, done){
			let rodada = 1
			const temporizador = setInterval(()=>{
				const novaLargura = this.larguraBase - rodada * 10
				el.style.width = `${novaLargura}px`
				rodada++
				if(rodada > 30){
					clearInterval(temporizador)
					done()
				}
			}, 20)			
		},
	}
	

}
</script>

<style>
#app {
	font-family: 'Avenir', Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
	margin-top: 60px;
	font-size: 1.5rem;
}
.caixa{
	height: 100px;
	width: 300px;
	margin: 30px auto;
	background-color: lightgreen;
}

.fade-enter, .fade-leave-to{
	opacity: 0;
}

.fade-enter-active, .fade-leave-active{
	transition: opacity 2s;
}
@keyframes slide-in {
	from { transform: translateY(40px); }
	to { transform: translateY(0);}
}

@keyframes slide-out {
	from { transform: translateY(0); }
	to { transform: translateY(40px);}
}


.slide-enter{
	opacity:0 ;
}

.slide-enter-to{
	transition: opacity 1.5s;
}

.slide-enter-active{
	animation: slide-in 2s ease;
}

.slide-leave-active{
	animation: slide-out 2s ease;
	transition: opacity 1.5s;
}
.slide-leave-to {
	opacity: 0;
}

</style>

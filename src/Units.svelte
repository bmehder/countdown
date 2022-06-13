<script>
	export let time
		
	const formattedUnit = (number, unit) => number === 1 ? unit : unit + 's'
</script>

<section>
	<div class="days">
		{time.days}<span>{formattedUnit(time.days, 'Day')}</span>
	</div>
	<div class="hours">
		{time.hours}<span>{formattedUnit(time.hours, 'Hour')}</span>
	</div>
	<div class="minutes">
		{time.minutes}<span>{formattedUnit(time.minutes, 'Minute')}</span>
	</div>
	<div class="seconds">
		{time.seconds}<span>{formattedUnit(time.seconds, 'Second')}</span>
	</div>
</section>

<style>
	section {
		display: flex;
		justify-content: center;
		align-items: center;
		gap: 1rem;
	}
	@media screen and (max-width: 600px) {
		section {
			flex-direction: column;
		}
	}
	div {
		width: 120px;
    height: 120px;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		border-radius: 50%;
    font-weight: bold;
		color: white;
		text-shadow: 0 0 1px #444;
		box-shadow: 0 20px 30px rgba(0, 0, 0, 0.24);
    background-image: linear-gradient(
      to bottom right,
      transparent,
      rgba(0, 0, 0, 0.05)
    );
		transform: scale(1);
		transition: transform 0.3s ease-in-out;
    animation: spin 1.2s ease-in-out;
	}
	div:hover {
    transform: scale(1.1);
  }
	.days {
		background-color: #10c45c;
	}
	.hours {
		background-color: #307ad5;
	}
	.minutes {
		background-color: #fdc735;
	}
	.seconds {
		background-color: #d94da6;
	}
	
	@keyframes spin {
    0% {
      transform: rotate(0deg);
      box-shadow: none;
      opacity: 0;
    }
    100% {
      transform: rotate3d(1, 1, 1, 360deg);
      opacity: 1;
    }
  }
</style>
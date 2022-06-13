<script>
  import Message from './Message.svelte'
  import Units from './Units.svelte'

  export let end = 'July 1, 2022 00:00:00 GMT'
  export let message = 'SALE ENDS IN'
  export let url = 'https://myfunscience.com/courses/'

  const ONE_SECOND = 1000
  const ONE_MINUTE = 1000 * 60
  const ONE_HOUR = 1000 * 60 * 60
  const ONE_DAY = 1000 * 60 * 60 * 24

  const endDate = new Date(end).getTime()

  let time = { seconds: null, minutes: null, hours: null, days: null }
  let intervalId

  $: isRunning = time.seconds || time.minutes || time.hours || time.days

  const setTime = timeLeft => {
    time.days = Math.floor(timeLeft / ONE_DAY)
    time.hours = Math.floor((timeLeft % ONE_DAY) / ONE_HOUR)
    time.minutes = Math.floor((timeLeft % ONE_HOUR) / ONE_MINUTE)
    time.seconds = Math.floor((timeLeft % ONE_MINUTE) / ONE_SECOND)
  }

  const countdown = () => {
    const now = new Date().getTime()
    const timeLeft = endDate - now

    if (timeLeft < 0) {
      clearInterval(intervalId)
      return
    }

    setTime(timeLeft)
  }

  const init = node => (intervalId = setInterval(countdown, ONE_SECOND))

  const handleClick = () => (window.location = url)
</script>

<aside use:init on:click={handleClick}>
  {#if isRunning}
    <Message {message} />
    <Units {time} />
  {/if}
</aside>

<style>
  aside {
    cursor: pointer;
  }
</style>

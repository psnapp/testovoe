<script>
import JSConfetti from 'js-confetti'
const confetti = new JSConfetti();

export default {
  mounted() {
    this.showConfetti();
  },
  methods: {
    showConfetti() {
      confetti.addConfetti({emojis: ['🧱', '🪚', '🛠', '🏗'],});
    },
  },
};
</script>

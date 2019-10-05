<script>
// CommitChart.js
import { Line } from 'vue-chartjs'

export default {
  extends: Line,
  mounted () {
    // Overwriting base render method with actual data.
    this.renderChart({
      labels: ['00.00', '03.20', '06.40', '10.00', '13.20', '16.40', '20.00'],
      datasets: [
        {
          label: 'Average Energy Production',
          backgroundColor: '#ffff4d',
          data: [0.0, 0.4, 0.7, 0.9, 1.5, 0.6, 0.3]
        }
      ]
    },
    {
      maintainAspectRatio: false
    })
  }
}
</script>

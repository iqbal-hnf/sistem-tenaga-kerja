<script>
    import { Instagram } from "svelte-bootstrap-icons";
</script>

<footer>
  <div class="footer-content">
    <div class="footer-item">
      <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit.</p>
    </div>
    <div class="footer-item">
      <p>Lorem ipsum</p>
      <p>Lorem ipsum</p>
      <p>Lorem ipsum</p>
    </div>
    <div class="footer-item">
      <p>Lorem ipsum</p>
      <p>Lorem ipsum</p>
      <p>Lorem ipsum</p>
    </div>
  </div>
  <div class="footer-bottom">
    <p>&copy; Lorem ipsum dolor sit amet</p>
    <div class="social-media">
      <a href="#"><img src="ala" alt="Facebook"></a>
      <a href="#"><img src="twitter-icon.png" alt="Twitter"></a>
      <a href="#"><Instagram /></a>
    </div>
  </div>
</footer>

<style>
  footer {
    background-color: #f8f8f8;
    padding: 20px;
  }

  .footer-content {
    display: flex;
    justify-content: space-between;
  }

  .footer-item {
    width: 30%;
  }

  .footer-bottom {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-top: 20px;
    border-top: 1px solid #ddd;
    padding-top: 10px;
  }

  .social-media img {
    width: 20px;
    height: 20px;
    margin-left: 10px;
  }
</style>

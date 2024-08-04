<script>
  // Import Bootstrap icons
  import { TelephoneFill, EnvelopeFill, GeoAltFill } from 'svelte-bootstrap-icons';
  import Navbar from '../../../components/Navbar.svelte';
  import 'bootstrap/dist/css/bootstrap.min.css';
</script>

<Navbar/>
<section class="company-info">
  <div class="container">
    <div class="row">
      <div class="col-md-6">
        <h2>About Our Company</h2>
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nullam auctor, est nec aliquam ultricies, ligula turpis vestibulum nisi, non placerat ex nisi et eros.</p>
        <p>Nam sodales condimentum nisl sed mattis. Cras in nisi sit amet dolor fermentum consectetur. Vivamus nec dui semper, feugiat urna nec, ultricies erat.</p>
      </div>
      <div class="col-md-6">
        <img src="https://via.placeholder.com/600x400" alt="Company Image" class="img-fluid">
      </div>
    </div>
  </div>
</section>

<section class="contact-info">
  <div class="container">
    <div class="row">
      <div class="col-md-4">
        <div class="card mb-4">
          <div class="card-body">
            <h5 class="card-title">Contact Information</h5>
            <ul class="list-unstyled">
              <li>
                <TelephoneFill class="icon" />
                <span>Phone: +123456789</span>
              </li>
              <li>
                <EnvelopeFill class="icon" />
                <span>Email: info@example.com</span>
              </li>
              <li>
                <GeoAltFill class="icon" />
                <span>Address: 123 Street, City, Country</span>
              </li>
            </ul>
          </div>
        </div>
      </div>
      <div class="col-md-8">
        <div class="card">
          <div class="card-body">
            <h5 class="card-title">Our Mission</h5>
            <p class="card-text">Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nullam auctor, est nec aliquam ultricies, ligula turpis vestibulum nisi, non placerat ex nisi et eros. Nam sodales condimentum nisl sed mattis. Cras in nisi sit amet dolor fermentum consectetur. Vivamus nec dui semper, feugiat urna nec, ultricies erat.</p>
            <p class="card-text">Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nullam auctor, est nec aliquam ultricies, ligula turpis vestibulum nisi, non placerat ex nisi et eros. Nam sodales condimentum nisl sed mattis. Cras in nisi sit amet dolor fermentum consectetur. Vivamus nec dui semper, feugiat urna nec, ultricies erat.</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>


<style>
  /* Custom CSS */
  .company-info {
    padding: 50px 0;
    background-color: #f8f9fa;
  }

  .about-section {
    margin-bottom: 50px;
  }

  .contact-info {
    background-color: #f8f9fa;
    padding: 50px 0;
  }

  .footer {
    background-color: #343a40;
    color: white;
    padding: 20px 0;
    text-align: center;
  }
</style>
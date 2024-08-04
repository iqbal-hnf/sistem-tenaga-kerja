<script>
    import Button from '../../../components/Button.svelte';
    // Data statis untuk profil
    let profile = {
      name: 'John Doe',
      email: 'john.doe@example.com',
      phone: '123-456-7890',
      dateOfBirth: '1985-10-25',
      location: 'New York, USA',
      summary: 'Experienced software developer with a strong background in full-stack development.',
      education: [
        { degree: 'B.Sc in Computer Science', institution: 'ABC University', year: '2007' }
      ],
      career: [{ title: 'Senior Developer', company: 'XYZ Corp', year: '2015-2020' }],
      certifications: [{ name: 'Certified Scrum Master', institution: 'Scrum Alliance' }],
      skills: ['JavaScript', 'React', 'Node.js'],
      languages: ['English', 'Spanish'],
      address: '123 Main St, New York, NY 10001',
      classification: 'Software Development'
    };
  
    function goBack() {
      window.history.back();
    }
  </script>
  
  <div class="profile-container">
    <h1>{profile.name}</h1>
    <p><strong>Email:</strong> {profile.email}</p>
    <p><strong>Phone:</strong> {profile.phone}</p>
    <p><strong>Date of Birth:</strong> {profile.dateOfBirth}</p>
    <p><strong>Location:</strong> {profile.location}</p>
  
    <div class="section">
      <h2>Personal Summary</h2>
      <p>{profile.summary}</p>
    </div>
  
    <div class="section">
      <h2>Education</h2>
      {#each profile.education as edu}
        <p>{edu.degree} from {edu.institution} ({edu.year})</p>
      {/each}
    </div>
  
    <div class="section">
      <h2>Career History</h2>
      {#each profile.career as job}
        <p>{job.title} at {job.company} ({job.year})</p>
      {/each}
    </div>
  
    <div class="section">
      <h2>Licenses and Certifications</h2>
      {#each profile.certifications as cert}
        <p>{cert.name} - {cert.institution}</p>
      {/each}
    </div>
  
    <div class="section">
      <h2>Skills</h2>
      <ul>
        {#each profile.skills as skill}
          <li>{skill}</li>
        {/each}
      </ul>
    </div>
  
    <div class="section">
      <h2>Languages</h2>
      <ul>
        {#each profile.languages as language}
          <li>{language}</li>
        {/each}
      </ul>
    </div>
  
    <div class="section">
      <h2>Address</h2>
      <p>{profile.address}</p>
    </div>
  
    <div class="section">
      <h2>Preferred Classification</h2>
      <p>{profile.classification}</p>
    </div>
  <div>
    <Button classList="btn-back">Kembali</Button>
  </div>
   
  </div>
  
  <style>
    .profile-container {
      max-width: 800px;
      margin: 0 auto;
      padding: 20px;
      border-radius: 8px;
      background-color: #f9f9f9;
      box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    }
  
    h1,
    h2 {
      color: #333;
    }
  
    .section {
      margin-bottom: 20px;
    }
  
    .section h2 {
      border-bottom: 2px solid #00195E;
      padding-bottom: 5px;
    }
  
    .section p {
      margin: 5px 0;
    }
  
    ul {
      list-style-type: none;
      padding: 0;
    }
  
    ul li {
      margin-bottom: 5px;
    }

  
    
  </style>
  
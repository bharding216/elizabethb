<script>
	import { page } from '$app/stores';

    const facebookLink = 'https://www.facebook.com/';
    const instagramLink = 'https://www.instagram.com/';
</script>

<footer>
    <div class="py-5 text-center">
        <div class="row pt-5 py-3">
            <div class="col-12">
                <a href={facebookLink} target="_blank" rel="noopener noreferrer" class="social-link fbook-link">
                    <i class="fab fa-facebook"></i>
                  </a>
                  
                  <a href={instagramLink} target="_blank" rel="noopener noreferrer" class="social-link">
                    <i class="fab fa-instagram"></i>
                  </a>
            </div>
        </div>
    
        <div class="row">
            <div class="col-12">
                <p>
                    &copy; 2023 Elizabeth B. Interiors
                </p>
            </div>
        </div>
    
        <div class="row">
            <div class="col-12">
                <p>
                    Site created by <a class="hover-link" href="https://www.getsurmount.com/"
                    target="_blank"
                    rel="noopener noreferrer">Surmount Web Development</a>
                </p>
            </div>
        </div>
    </div>
</footer>


<style>
  .social-link {
    font-size: 36px;
  }

  .fbook-link {
    margin-right: 30px;
  }

</style>

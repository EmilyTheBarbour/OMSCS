Loads can start early before a branch outcome is known

Once the branch outcome is known, Either:
- Commit the load
- Throw it away

Loads have latencies, so its better to try and keep loading as much as possible then blocking on a latent load.
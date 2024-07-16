1. **Install APCu PHP Extension**:
   ```bash
   sudo apt-get install php7.4-apcu
   ```

2. **Download Object Cache Script**:
   ```bash
   wget https://raw.githubusercontent.com/l3rady/object-cache-apcu/main/object-cache.php -O /path/to/site/wp-content/object-cache.php
   ```

3. **Edit PHP Configuration Files**:
   ```bash
   sudo nano /etc/php/7.4/cli/php.ini
   sudo nano /etc/php/7.4/fpm/php.ini
   ```

4. **Add APCu Configuration**:
   Add the following lines to the end of both `php.ini` files:
   ```ini
   [apcu]
   apc.enabled=1
   apc.shm_size=512M  ; Increase the shared memory size
   apc.ttl=3600       ; Set a reasonable time to live for cache entries in seconds
   apc.gc_ttl=3600    ; Garbage collection time to live
   apc.entries_hint=4096 ; Estimated number of cache entries
   apc.slam_defense=1 ; Prevent cache stampede
   apc.serializer=php ; Default serializer
   apc.enable_cli=1   ; Enable APCu for CLI (optional)
   apc.stat=1         ; Enable update of cached files. Disable for production.
   ```

5. **Configure WordPress**:
   Add the following lines to your `wp-config.php` file, ensuring you use a different salt key for each site:
   ```php
   define('WP_APCU_KEY_SALT', 'random-32-characters'); # cat /dev/urandom | LC_ALL=C tr -dc 'A-Za-z0-9' | fold -w 32 | head -n 10 on mac
   define('WP_APCU_LOCAL_CACHE', true);
   ```

# Role apache

Ce role installe Apache et deploie un virtualhost pour Drupal.

## Variables

- `apache_package_ubuntu`
- `apache_package_rocky`
- `apache_service_ubuntu`
- `apache_service_rocky`

## Exemple

```yaml
- role: junkojv.drupal.apache
```

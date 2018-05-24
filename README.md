# docker-openldap
OpenLDAP container containing schema for Postfix and Samba integration.

Also contains a `default-structure.ldif` script for a basic OU creation (located at the root of the filesystem */* ).
After running the container, run the following command to create the structure:
```
docker exec openldap ldapadd -H ldap://127.0.0.1 -x -D "cn=admin,dc=exmple,dc=com" -f /default-structure.ldif -w P@$$w0rd
```

## Sample `docker run`
```
docker run --detach \
--env LDAP_ORGANISATION="EXAMPLE" \
--env LDAP_DOMAIN="example.com" \
--env LDAP_ADMIN_PASSWORD="P@$$w0rd" \
--name openldap \
--volume /share/ldap/var/lib/ldap:/var/lib/ldap \
--volume /share/ldap/etc/ldap/slapd:/etc/ldap/slapd.d \
--volume /share/ldap/container/service/slapd/assets/certs:/container/service/slapd/assets/certs \
--volume /share/ldap/share:/share \
cajetan19/openldap
```

## Disclaimer

This image makes use of the [jsmitsnl/docker-openldap-postfix-book](https://github.com/johansmitsnl/docker-openldap-postfix-book) and the [osixia/openldap](https://hub.docker.com/r/osixia/openldap/) images. For more information about environment variables, refer to their respective images.

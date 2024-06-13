# Unix Pass

## Generate gpg key
- Create
```bash
gpg gen-key
```

- Edit to remove expiration date
```bash
gpg --edit-key PUB_KEY
gpg> expire
gpg> save
```

## Init storage
- Init pass
```bash
pass init PUB_KEY
```

- Init git
```bash
pass git init
```

## Create password
- By user
```bash
pass insert name
```

- Generated password
```bash
pass generate name
```

## Export keys
- Public
```bash
gpg --output public.pgp --armor --export hola@com
```

- Private
```bash
gpg --output private.pgp --armor --export-secret-key hola@com
```

## Import keys
```bash
gpg --import private.pgp
gpg --import public.pgp
```

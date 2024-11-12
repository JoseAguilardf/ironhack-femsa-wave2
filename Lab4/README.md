## Escenarios para el diseño de seguridad:

***Escenario 1: Pseudocódigo para el sistema de autenticación***

      FUNCTION authenticateUser(username, password):
        QUERY database WITH username AND password
        IF found RETURN True
        ELSE RETURN False


***Vulnerabilidades:***

  Consulta no parametrizada
  Almacenamiento inseguro; un atacante podría acceder a las contraseñas sin cifrado.
  Sin límite de intentos fallidos


***Mejoras:***

  Consultas parametrizadas, hash de contraseñas, límite de intentos fallidos, registro de eventos y mensajes de error genéricos.


      FUNCTION secureAuthenticate(username, password):
        IF isTemporarilyBlocked(username):
          RETURN "Cuenta temporalmente bloqueada"

        # Convertir la contraseña a hash para no compararla en texto plano
        hashedPassword = hash(password)

        # Consulta a la base de datos usando parámetros seguros para evitar inyecciones SQL
        QUERY "SELECT 1 FROM users WHERE username = ? AND password = ?" WITH PARAMETERS (username, hashedPassword)

        IF userExists:
          resetFailedLogin(username)  # Restablece intentos fallidos después de inicio exitoso
          RETURN "Inicio de sesión exitoso"
        ELSE:
          increaseFailedLogin(username)  # Aumenta los intentos fallidos
          IF getFailedLoginCount(username) >= 3:
            blockTemporarily(username)  # Bloquea temporalmente si hay demasiados intentos fallidos
          RETURN "Credenciales incorrectas"

***Escenario 2: Esquema de autenticación JWT***

      DEFINE FUNCTION generateJWT(userCredentials):
        IF validateCredentials(userCredentials):
          SET tokenExpiration = currentTime + 3600 // Token expires in one hour
          RETURN encrypt(userCredentials + tokenExpiration, secretKey)
        ELSE:
          RETURN error

***Vulnerabilidades***

  Tokens largos incrementan el riesgo de uso no autorizado
  Sin mecanismos para confirmar la integridad del token, podría manipularse.
  El token es válido hasta que expire, sin control en caso de compromiso.

***Mejoras:***

  Clave segura, expiración corta, firma digital del token

      FUNCTION generateSecureJWT(userCredentials):
        IF validateUserCredentials(userCredentials):
          tokenExpiration = currentTime + 1800  # Expira en 30 minutos para mayor seguridad
          tokenPayload = userCredentials + tokenExpiration
          jwtToken = signWithSecretKey(tokenPayload, secureSecretKey)  # Firma el token con clave segura
          RETURN jwtToken
        ELSE:
          RETURN "Credenciales inválidas"
      
      FUNCTION validateJWT(jwtToken):
        IF isTokenRevoked(jwtToken):
          RETURN "Token inválido"
      
        decodedPayload = decodeWithSecretKey(jwtToken, secureSecretKey)  # Decodifica con clave segura
        IF decodedPayload.expiration < currentTime:
          RETURN "Token expirado"
        ELSE:
          RETURN "Token válido"

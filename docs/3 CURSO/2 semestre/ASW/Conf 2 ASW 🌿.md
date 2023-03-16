- **Tests de integración**: pruebas que comprueban que todos los componentes del software funcionan juntos de forma correcta
- **Latecy tolerance**: tenemos un sistema que envía información a otros nodos, cuando esos nodos responden lentamente, se puede llegar a acumular esa información y bloquearse. Para esto existe el **circuit breaker** (Hystrix (*deprecated*) -> RESILIENCE4J), que para temporalmente el sistema y después vuelve a probar a ver si puede reenviar la información.

---
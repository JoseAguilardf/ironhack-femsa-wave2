openapi: 3.0.0
info:
  title: API de Carrito de Compras Básico
  description: API para gestionar cuentas de usuario, añadir productos al carrito y procesar pedidos.
  version: 1.0.0

servers:
  - url: https://api.mitiendita.com/v1
    description: API Principal
tags:
  - name: Usuarios
    description: Operaciones de registro e inicio de sesión de usuarios
  - name: Carrito
    description: Operaciones relacionadas con el carrito de compra
paths:
  /usuarios:
    post:
      summary: Crear usuario
      description: Crea una cuenta de usuario con nombre y correo electrónico.
      tags:
        - Usuarios  
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/UsuarioInput'
      responses:
        '201':
          description: Usuario creado
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Usuario'

  /carrito/{usuarioId}:
    get:
      summary: Ver carrito
      description: Retorna los productos actuales en el carrito de un usuario.
      tags:
        - Carrito  
      parameters:
        - name: usuarioId
          in: path
          required: true
          schema:
            type: string
      responses:
        '200':
          description: Carrito actual del usuario
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Carrito'
    post:
      summary: Agregar producto al carrito
      description: Añade un producto específico al carrito de un usuario.
      tags:
        - Carrito 
      parameters:
        - name: usuarioId
          in: path
          required: true
          schema:
            type: string
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/ProductoCarrito'
      responses:
        '200':
          description: Producto agregado exitosamente al carrito

  /pedidos:
    post:
      summary: Crear pedido
      description: Convierte el carrito de un usuario en un pedido procesado.
      tags:
        - Pedidos 
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/PedidoInput'
      responses:
        '201':
          description: Pedido creado y en proceso
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Pedido'

components:
  schemas:
    Usuario:
      type: object
      properties:
        id:
          type: string
        nombre:
          type: string
        email:
          type: string

    UsuarioInput:
      type: object
      properties:
        nombre:
          type: string
        email:
          type: string
        password:
          type: string

    Carrito:
      type: object
      properties:
        usuarioId:
          type: string
        productos:
          type: array
          items:
            $ref: '#/components/schemas/ProductoCarrito'
        total:
          type: number
          format: float

    ProductoCarrito:
      type: object
      properties:
        productoId:
          type: string
        cantidad:
          type: integer

    Pedido:
      type: object
      properties:
        id:
          type: string
        usuarioId:
          type: string
        productos:
          type: array
          items:
            $ref: '#/components/schemas/ProductoCarrito'
        total:
          type: number
          format: float
        estado:
          type: string
          enum: ["pendiente", "procesado", "enviado"]

    PedidoInput:
      type: object
      properties:
        usuarioId:
          type: string
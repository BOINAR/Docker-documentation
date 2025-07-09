services:
  db:
    image: postgres:16
    container_name: postgres-db
    restart: unless-stopped
    env_file:
      - .env
    volumes:
      - pgdata:/var/lib/postgresql/data
    ports:
      - "5432:5432"
    networks:
      - app-network

  backend:
    build:
      context: ./backend
    image: backend:1.0.0
    container_name: nest-backend
    restart: unless-stopped
    env_file:
      - .env
    depends_on:
      - db
    ports:
      - "3001:3001"
    networks:
      - app-network

  frontend:
    build:
      context: ./frontend
    image: frontend:1.0.0
    container_name: next-frontend
    restart: unless-stopped
    env_file:
      - .env
    depends_on:
      - backend
    ports:
      - "3000:3000"
    networks:
      - app-network

volumes:
  pgdata:

networks:
  app-network:

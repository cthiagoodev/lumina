# 📸 Lumina

> **Secure photo delivery and client galleries for photographers.** > An event-driven photo delivery platform built with Kotlin, Kafka, and Rust.

[![License: AGPL v3](https://img.shields.io/badge/License-AGPL%20v3-blue.svg)](https://www.gnu.org/licenses/agpl-3.0)
[![Kotlin](https://img.shields.io/badge/kotlin-%237F52FF.svg?style=flat&logo=kotlin&logoColor=white)](https://kotlinlang.org/)
[![Spring Boot](https://img.shields.io/badge/spring-%236DB33F.svg?style=flat&logo=spring&logoColor=white)](https://spring.io/projects/spring-boot)
[![Rust](https://img.shields.io/badge/rust-%23000000.svg?style=flat&logo=rust&logoColor=white)](https://www.rust-lang.org/)
[![Apache Kafka](https://img.shields.io/badge/Apache%20Kafka-000?style=flat&logo=apachekafka)](https://kafka.apache.org/)
[![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=flat&logo=docker&logoColor=white)](https://www.docker.com/)

O **Lumina** é um SaaS (Software as a Service) open-source projetado para resolver a dor crônica de fotógrafos profissionais: entregar ensaios fotográficos de forma elegante, segura contra roubos (prints) e automatizada.

## ✨ Principais Funcionalidades

* **🔒 Proteção por Marca d'Água:** O cliente visualiza apenas *previews* otimizados e protegidos com marca d'água.
* **📦 Imutabilidade da Origem:** Os arquivos originais em alta resolução nunca são expostos na vitrine web até o download ser explicitamente liberado.
* **⏳ Links Efêmeros:** Otimização de armazenamento através de galerias que expiram.
* **⚡ Processamento Assíncrono:** Redimensionamento de imagem e aplicação de marca d'água desacoplados, processados por um Worker de alta performance em Rust via Apache Kafka.
* **☁️ Cloud-Native Storage:** Compatibilidade 100% com a API S3 (MinIO para desenvolvimento local, Cloudflare R2/AWS S3 para produção).

## 🏗️ Arquitetura do Sistema

O Lumina utiliza uma arquitetura de microsserviços orientada a eventos para garantir escalabilidade no processamento pesado de imagens.

* **API (Cérebro):** Kotlin + Spring Boot
* **Frontend (Vitrine):** Jaspr (Dart)
* **Mensageria:** Apache Kafka (Modo KRaft)
* **Worker (Processamento):** Rust
* **Banco de Dados:** PostgreSQL
* **Object Storage:** MinIO / AWS S3
* **Proxy Reverso:** Nginx

📖 **Documentação Completa:** O detalhamento visual da arquitetura (C4 Model), Diagrama de Banco de Dados (ERD) e Fluxogramas de Infraestrutura podem ser encontrados abrindo o arquivo `docs/index.html` no seu navegador.

## 🚀 Como rodar o projeto localmente

### 1. Pré-requisitos
* [Docker](https://www.docker.com/) e Docker Compose instalados.
* JDK 25+ (Para o Spring Boot)
* Rust e Cargo (Para o Worker)

### 2. Subindo a Infraestrutura (PostgreSQL, Kafka e MinIO)

Clone o repositório e suba os containers isolados na rede Docker:

```bash
git clone git@github.com:cthiagoodev/lumina.git
cd lumina
docker compose up -d
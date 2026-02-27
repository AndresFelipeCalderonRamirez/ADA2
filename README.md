# ADA2

1. Introducción

En EcoStream, startup SaaS enfocada en gestión de huella de carbono industrial, el nuevo módulo de Análisis Predictivo y Reporteo Automatizado requiere acelerar el SDLC sin comprometer calidad, seguridad ni escalabilidad.

Como Lead Prompt Engineer, se diseñó una estrategia integral de Ingeniería de Prompts aplicada a todas las fases del SDLC:

Análisis de Requisitos

Arquitectura

Generación de Código

Refactorización

Testing

Seguridad

Documentación

FASE 1: Análisis y Planificación (Zero-Shot + Few-Shot)
1.1 System Prompt – Agente Analista de Negocios Senior

Técnica: Zero-Shot con Role Prompting

Prompt Diseñado
SYSTEM PROMPT:

Actúa como un Analista de Negocios Senior especializado en plataformas SaaS industriales y soluciones de sostenibilidad ambiental.

Tu objetivo es:
- Traducir necesidades empresariales en requisitos funcionales claros.
- Identificar riesgos técnicos y regulatorios.
- Priorizar funcionalidades basadas en impacto y viabilidad.
- Considerar cumplimiento normativo ambiental (ej. ISO 14064).

Responde de forma estructurada:
1. Contexto
2. Problema
3. Requisitos Funcionales
4. Riesgos
5. Métricas de Éxito
Resultado Obtenido (Fragmento)

Identificación de necesidad de predicción de emisiones basada en series temporales.

Inclusión de cumplimiento normativo.

Recomendación de dashboards exportables en PDF/CSV.

Métrica propuesta: reducción del 30% en tiempo de generación de reportes.

1.2 Generación de 5 Requisitos Funcionales

Técnica: Few-Shot Prompting

Prompt Diseñado
Genera requisitos funcionales siguiendo el formato de ejemplo:

Ejemplo 1:
RF-01: El sistema debe permitir cargar datos históricos de emisiones en formato CSV.

Ejemplo 2:
RF-02: El sistema debe generar reportes mensuales automáticos en PDF.

Ahora genera 5 nuevos requisitos funcionales para un módulo de análisis predictivo de huella de carbono.
Resultado Obtenido

RF-03: El sistema debe predecir emisiones futuras usando modelos de series temporales.
RF-04: El sistema debe generar alertas cuando se proyecte un exceso sobre metas ambientales.
RF-05: El sistema debe permitir simulaciones de escenarios.
RF-06: El sistema debe exportar reportes en formatos compatibles con auditorías regulatorias.
RF-07: El sistema debe registrar logs auditables de predicciones generadas.

Justificación Técnica

Role Prompting mejora consistencia y reduce ambigüedad.

Few-Shot mitiga alucinaciones estructurales.

Formato explícito evita outputs vagos.

FASE 2: Arquitectura y Diseño (Chain-of-Thought)
2.1 Prompt de Arquitectura con CoT

Técnica: Chain-of-Thought + Structured Reasoning

Prompt Diseñado
Actúa como Arquitecto de Software Senior.

Paso 1: Identifica los componentes necesarios para un módulo de análisis predictivo en una plataforma SaaS.
Paso 2: Define cómo se comunicarán (API Gateway, eventos, etc.).
Paso 3: Considera escalabilidad horizontal.
Paso 4: Incorpora medidas de seguridad (OAuth2, cifrado, aislamiento).
Paso 5: Presenta la arquitectura final en formato estructurado.

Contexto: Plataforma SaaS industrial multi-tenant con datos sensibles ambientales.
Resultado Obtenido (Resumen)

Arquitectura propuesta:

API Gateway

Microservicio de Ingesta de Datos

Microservicio de Modelado Predictivo (ML Service)

Servicio de Reportes

Base de Datos PostgreSQL

Almacenamiento en S3

Servicio de Autenticación (OAuth2/JWT)

Incluyó:

Comunicación vía REST + eventos (Kafka)

Multi-tenancy con aislamiento lógico

Cifrado en tránsito (TLS 1.3)

Contenedores Docker + Kubernetes

Justificación Técnica

CoT obliga razonamiento paso a paso.

Reduce respuestas superficiales.

Mejora coherencia arquitectónica.

Disminuye riesgo de omitir aspectos críticos como seguridad.

FASE 3: Generación de Código y Refactorización
3.1 Boilerplate API – FastAPI

Técnica: Zero-Shot estructurado

Prompt Diseñado
Genera el boilerplate de una API REST en Python usando FastAPI.

Requisitos:
- Endpoint POST /predict
- Recibe datos históricos en JSON
- Devuelve predicción simulada
- Manejo básico de errores
- Validación con Pydantic
- Código listo para producción (estructura limpia)
Resultado Obtenido (Fragmento)
from fastapi import FastAPI, HTTPException
from pydantic import BaseModel
from typing import List

app = FastAPI()

class EmissionData(BaseModel):
    values: List[float]

@app.post("/predict")
def predict(data: EmissionData):
    if not data.values:
        raise HTTPException(status_code=400, detail="No data provided")
    
    prediction = sum(data.values) / len(data.values)
    return {"prediction": prediction}
3.2 Prompt de Refactorización

Técnica: Code Review Prompting

Prompt Diseñado
Refactoriza el siguiente código para:
- Mejorar legibilidad
- Separar lógica de negocio
- Seguir principios SOLID
- Manejar errores correctamente

[PEGAR CÓDIGO]
Resultado Obtenido

Separación en:

router.py

service.py

models.py

Inclusión de try/except

Mejora en validación

Justificación Técnica

Prompts específicos reducen código inseguro.

Solicitar principios SOLID mejora mantenibilidad.

Separación por capas reduce deuda técnica futura.

FASE 4: Testing, Seguridad y Documentación
4.1 Prompt para Unit Tests

Técnica: Zero-Shot estructurado

Genera una suite de pruebas unitarias usando pytest para la API FastAPI.

Incluye:
- Test para predicción correcta
- Test para lista vacía
- Test para input inválido
- Cobertura mínima del 80%
Resultado (Fragmento)
def test_prediction_valid():
    response = client.post("/predict", json={"values": [10,20,30]})
    assert response.status_code == 200
    assert response.json()["prediction"] == 20
4.2 Prompt de Red Teaming (Seguridad)

Técnica: Adversarial Prompting

Actúa como un experto en ciberseguridad.

Analiza el siguiente código y detecta:
- Riesgos de inyección SQL
- Exposición de datos sensibles
- Falta de validación
- Problemas de autenticación

Sugiere correcciones específicas.
Resultado

La IA detectó:

Falta de autenticación JWT

Ausencia de rate limiting

Riesgo potencial si se conecta a DB sin ORM parametrizado

Justificación Técnica

Red Team Prompt reduce vulnerabilidades.

Mitiga riesgo de código inseguro generado por IA.

Mejora cumplimiento de estándares OWASP.
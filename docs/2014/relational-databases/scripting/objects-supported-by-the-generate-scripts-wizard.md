---
title: Objetos com suporte no Assistente para Gerar Scripts
ms.custom: seo-lt-2019
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 071eb2cb-f073-41ca-9f4d-11d3b8803495
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 1cfee492433da4a9812a6961d34b741cf8bff089
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82703819"
---
# <a name="objects-supported-by-the-generate-scripts-wizard"></a>Objetos com suporte no Assistente para Gerar Scripts
  O Assistente para Gerar e Publicar Scripts oferece suporte a um subconjunto dos objetos com suporte no [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
## <a name="supported-objects"></a>Objetos com suporte  
 A seguinte tabela lista os objetos que podem ser publicados e as versões com suporte do Assistente para Gerar e Publicar Scripts.  
  
||||||  
|-|-|-|-|-|  
|Função de aplicativo|Função de banco de dados|Esquema|Agregação definida pelo usuário|Exibição<sup>1</sup>|  
|Assembly|Restrição DEFAULT|Procedimento armazenado<sup>1</sup>|Tipo de dados definido pelo usuário|Coleção de esquemas XML|  
|Restrição CHECK|Catálogo de texto completo|Sinônimo|Função definida pelo usuário||  
|Procedimento armazenado do CLR (Common Language Runtime)<sup>1</sup>|Índice|Tabela|Tabela definida pelo usuário||  
|Função CLR definida pelo usuário|Regra|Usuário<sup>2</sup>|Tipo definido pelo usuário||  
  
 <sup>1</sup> publicado sem criptografia.  
  
 <sup>2</sup> os usuários que não são do sistema existentes no banco de dados são publicados como funções.  
  
  

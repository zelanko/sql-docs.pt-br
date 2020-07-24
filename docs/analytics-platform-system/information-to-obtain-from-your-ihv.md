---
title: Obter informações do IHV
description: Informações a serem obtidas do seu IHV sobre o dispositivo de sistema de plataforma de análise.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 29d243ccb58240bce0ce637c1e9e44b12009a2a4
ms.sourcegitcommit: 591bbf4c7e4e2092f8abda6a2ffed263cb61c585
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86942511"
---
# <a name="information-to-obtain-from-your-ihv"></a>Informações a serem obtidas do seu IHV
Quando o seu fornecedor independente de hardware (IHV) entrega seu novo dispositivo de SQL Server PDW para você, ele também fornecerá informações sobre o hardware do dispositivo e a configuração que eles executaram em seu dispositivo. Você precisará dessas informações para administrar seu dispositivo.  
  
A lista a seguir mostra informações que geralmente são necessárias do seu IHV. Em alguns casos, outras informações são necessárias. Verifique com seu IHV para ter certeza de que todas as informações relevantes foram transferidas para você com a entrega do dispositivo.  
  
|Informações ou documento|Descrição|
|-|-|
|Lista de materiais (BOM)|Sua lista de materiais lista os componentes que estão incluídos em seu dispositivo. Essas informações são necessárias para confirmar que todos os componentes foram entregues.<br /><br />**Importante:** Sua lista de materiais deve incluir pesos para cada um dos nós de dispositivo e para cada rack completo. Essas informações são importantes ao planejar como lidar e mover componentes de dispositivo e para garantir que seus data center possam acomodar o dispositivo. Se a sua BOM não incluir pesos de nó, certifique-se de obter essas informações do seu IHV para todos os nós.|  
|Diagramas de cabeamento|Os diagramas de cabeamento mostram como conectar a rede, a energia e outros cabos para cada rack de dispositivo. Esses diagramas são necessários ao instalar o dispositivo em seu data center e sempre que você precisar remover ou substituir um componente.|  
|Requisitos de rack de dispositivo|Antes que seu dispositivo possa ser instalado em seu data center, você precisa saber se suas data center atendem aos requisitos de fluxo de ar e comprimento de cabo para o dispositivo, bem como os requisitos de tamanho e energia para os componentes. Consulte também a BOM (lista de materiais) acima para obter informações sobre os pesos dos componentes do dispositivo, o que também é necessário.|  
  

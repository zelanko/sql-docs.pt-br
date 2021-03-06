---
description: Tipos definidos pelo usuário
title: Tipos definidos pelo usuário | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 19a71b27-b788-43a3-a76d-fe3001a6f016
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 04c7d143e24efbd21e977c1538820e1cb2289049
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487975"
---
# <a name="user-defined-types"></a>Tipos definidos pelo usuário

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Os UDTs (tipos definidos pelo usuário) foram introduzidos no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] para permitir que os desenvolvedores estendessem o sistema de tipo escalar do servidor armazenando objetos de CLR (Common Language Runtime) em um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os UDTs podem conter vários elementos e ter comportamentos, diferentemente dos tipos de dados de alias tradicionais, que consistem em um único tipo de dados do sistema no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os UDTs eram anteriormente restritas a um tamanho máximo de 8 kilobytes. No [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)], o suporte foi adicionado a UDTs maiores que 64 quilobytes. A partir da versão 3.0, o JDBC Driver também oferece suporte a UDTs com mais de 64 kilobytes quando você especifica o formato UserDefined.

Não há alteração de comportamento para UDTs inferiores ou iguais a 8.000 bytes, mas são suportados UDTs maiores que informam seu tamanho como "ilimitado".

## <a name="see-also"></a>Confira também

[Noções básicas sobre os tipos de dados do JDBC Driver](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)

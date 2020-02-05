---
title: Configurar um firewall para acesso ao FILESTREAM | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- Windows Firewall [Database Engine], FILESTREAM
- FILESTREAM [SQL Server], Windows Firewall
ms.assetid: fc52007f-c26f-4f8e-b9d8-55a7978f4d56
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 94df8085482c48d02e1e174ade2207ddad494acb
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68085431"
---
# <a name="configure-a-firewall-for-filestream-access"></a>Configurar um firewall para acesso ao FILESTREAM
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Para usar FILESTREAM em um ambiente protegido por firewall, o cliente e o servidor devem poder resolver nomes DNS para o servidor que contém os arquivos de FILESTREAM. O FILESTREAM exige que as portas de compartilhamento de arquivos do Windows 139 e 445 estejam abertas.  
  
### <a name="to-open-the-windows-file-sharing-ports-on-a-computer-that-is-running-windows-7"></a>Para abrir as portas de compartilhamento de arquivos do Windows em um computador que está executando o Windows 7  
  
1.  No Painel de Controle, abra o **Firewall do Windows**.  
  
2.  No painel esquerdo, clique em **Configurações avançadas**. Se você for solicitado para uma senha de administrador ou confirmação, digite a senha ou forneça a confirmação.  
  
3.  Na caixa de diálogo **Firewall do Windows com Segurança Avançada** , no painel esquerdo, clique em **Regras de Entrada**e, no painel direito, clique em **Nova Regra**.  
  
4.  Siga as instruções do assistente Nova Regra de Entrada para adicionar a porta TCP 139.  
  
5.  Repita a etapa anterior para adicionar a porta TCP 445.  
  
6.  Feche a caixa de diálogo **Firewall do Windows com Segurança Avançada** .  
  
  

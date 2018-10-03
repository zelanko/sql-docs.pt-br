---
title: Práticas recomendadas para o Assistente de migração de dados (SQL Server) | Microsoft Docs
description: Conheça as práticas recomendadas para migrar bancos de dados do SQL Server com o Assistente de migração de dados
ms.custom: ''
ms.date: 08/29/2018
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Best Practices
ms.assetid: ''
author: HJToland3
ms.author: rajpo
manager: craigg
ms.openlocfilehash: 9a8d346e3cc4a2ddc718d9e2758ec02caa458a8f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47632687"
---
# <a name="best-practices-for-running-data-migration-assistant"></a>Práticas recomendadas para executar o Assistente de migração de dados
Este artigo fornece algumas informações de prática recomendadas para instalação, avaliação e migração.

## <a name="installation"></a>Instalação
Não instalar e executar o Assistente de migração de dados diretamente no computador de host do SQL Server.

## <a name="assessment"></a>Avaliação
- Execute avaliações em bancos de dados de produção durante horários de pico.
- Executar o **problemas de compatibilidade** e **nova recomendação de recurso** avaliações separadamente para reduzir a duração de avaliação.

## <a name="migration"></a>Migração
- Migre um servidor durante horários de pico.

- Ao migrar um banco de dados, forneça um local único compartilhamento acessível pelo servidor de origem e o servidor de destino e evite uma operação de cópia, se possível. Uma operação de cópia pode introduzir um atraso de acordo com o tamanho do arquivo de backup. A operação de cópia também aumenta as chances de que a migração falhará devido a uma etapa extra. Quando um único local é fornecido, o Assistente de migração de dados ignora a operação de cópia.
 
    Além disso, certifique-se que, para fornecer as permissões corretas para a pasta compartilhada para evitar falhas de migração. As permissões corretas são especificadas na ferramenta. Se uma instância do SQL Server for executado com credenciais de serviço de rede, conceda as permissões corretas na pasta compartilhada para a conta do computador para a instância do SQL Server.

- Habilitar criptografar a conexão ao se conectar a servidores de origem e destino. Usando o SSL a criptografia aumenta a segurança dos dados transmitidos pelas redes entre o Assistente de migração de dados e a instância do SQL Server, que é útil especialmente ao migrar logons do SQL Server. Se a criptografia SSL não é usada e a rede estiver comprometida por um invasor, os logons do SQL que está sendo migrados poderia obter interceptados e/ou modificado em dinamicamente pelo invasor.

    No entanto, se todos os acessos envolverem uma configuração de intranet segura, a criptografia poderá não ser necessária. Habilitação da criptografia reduz o desempenho porque a sobrecarga extra que é necessária para criptografar e descriptografar os pacotes. Para obter mais informações, consulte [criptografando conexões com o SQL Server](https://go.microsoft.com/fwlink/?linkid=832513).

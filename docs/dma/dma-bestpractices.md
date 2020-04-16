---
title: Melhores práticas para o Assistente de Migração de Dados
description: Aprenda as melhores práticas para migrar bancos de dados SQL Server com o Assistente de Migração de Dados
ms.custom: seo-lt-2019
ms.date: 03/12/2019
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
ms.openlocfilehash: f2bfbb79a8a4803bb56e3dce85f575e8cf257b4a
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388158"
---
# <a name="best-practices-for-running-data-migration-assistant"></a>Práticas recomendadas para executar o Assistente de Migração de Dados
Este artigo fornece algumas informações de boas práticas para instalação, avaliação e migração.

## <a name="installation"></a>Instalação
Não instale e execute o Assistente de Migração de Dados diretamente na máquina host do SQL Server.

## <a name="assessment"></a>Avaliação
- Executar avaliações em bancos de dados de produção durante os horários de pico.
- Realize os **problemas de compatibilidade** e **novas avaliações de recomendações de recursos** separadamente para reduzir a duração da avaliação.

## <a name="migration"></a>Migração
- Migre um servidor durante os horários de não pico.

- Ao migrar um banco de dados, forneça um único local de compartilhamento acessível pelo servidor de origem e pelo servidor de destino e evite uma operação de cópia, se possível. Uma operação de cópia pode introduzir atraso com base no tamanho do arquivo de backup. A operação de cópia também aumenta as chances de uma migração falhar por causa de um passo extra. Quando um único local é fornecido, o Assistente de Migração de Dados ignora a operação de cópia.
 
    Além disso, certifique-se de fornecer as permissões corretas à pasta compartilhada para evitar falhas de migração. As permissões corretas são especificadas na ferramenta. Se uma instância do SQL Server for executada sob credenciais do Serviço de Rede, dê as permissões corretas na pasta compartilhada para a conta da máquina para a instância do SQL Server.

- Habilite a conexão criptografada ao se conectar aos servidores de origem e destino. O uso da criptografia TLS aumenta a segurança dos dados transmitidos entre as redes entre o Data Migration Assistant e a instância sql server, o que é benéfico especialmente ao migrar logins SQL. Se a criptografia TLS não for usada e a rede for comprometida por um invasor, os logins SQL que estão sendo migrados poderão ser interceptados e/ou modificados no voo pelo invasor.

    No entanto, se todos os acessos envolverem uma configuração de intranet segura, a criptografia poderá não ser necessária. A ativação da criptografia diminui o desempenho porque a sobrecarga extra necessária para criptografar e descriptografar pacotes. Para obter mais informações, consulte [As conexões criptografadas no SQL Server](https://go.microsoft.com/fwlink/?linkid=832513).
    
- Verifique se há restrições não confiáveis no banco de dados de origem e no banco de dados de destino antes de migrar dados. Após a migração, analise novamente o banco de dados de destino para ver se alguma restrição se tornou não confiável como parte da movimentação de dados. Corrigir restrições não confiáveis conforme necessário. Deixar as restrições não confiáveis pode resultar em planos de execução ruins, e isso pode afetar o desempenho.

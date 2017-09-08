---
title: "Pacotes instalados em bibliotecas de usuário | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 99ffd9b8-aa6d-4ac2-9840-4e66d0463978
caps.latest.revision: 2
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b4d5c7f3d1d0da5e1967140fcbdfcf60ba4571e7
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="packages-installed-in-user-libraries"></a>Pacotes instalados em bibliotecas de usuário

Se um usuário precisar de um novo pacote de R e não for um administrador, os pacotes não poderão ser instalados no local padrão e serão, por padrão, instalados em uma biblioteca do usuário privada. 

Em um ambiente de desenvolvimento típico do R, para referenciar o pacote no código, o usuário teria que adicionar o local para a variável de ambiente `libPath` do R ou então referenciar o caminho completo do pacote, deste modo:  
  
~~~~
library("c:/Users/<username>/R/win-library/packagename")  
~~~~

## <a name="problems-with-packages-in-user-libraries"></a>Problemas com pacotes em bibliotecas de usuário

No entanto, em [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], essa solução **não** tem suporte; os pacotes devem ser instalados na biblioteca padrão. Se o pacote não estiver instalado na biblioteca padrão, você poderá receber esse erro ao tentar chamar o pacote:

*Erro em library(xxx): não há nenhum pacote chamado 'xxx'*
 

Portanto, ao migrar soluções de R para serem executadas em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], é importante que você faça o seguinte:
+ Instale quaisquer pacotes de que você precise na biblioteca padrão.
+ Edite o código para garantir que os pacotes sejam carregados da biblioteca padrão e não de diretórios ad hoc ou bibliotecas de usuário.
+ Verifique seu código para certificar-se de que não há nenhuma chamada para pacotes desinstalados.
+ Modifique qualquer código que tentaria instalar pacotes dinamicamente.
 
Se um pacote estiver instalado na biblioteca padrão, o tempo de execução de R carregará o pacote da biblioteca padrão, mesmo que uma biblioteca diferente esteja especificada no código R.

## <a name="see-also"></a>Consulte também

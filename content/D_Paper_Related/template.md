---
draft: true
---

---date: {% if date %}{{date | format("YYYY-MM")}}{% endif %}---





# 论文信息

**Title:** {{title}}
**Authors:** {% for t in creators %}{{t.firstName}}{{t.lastName}}{{t.name}}{% if not loop.last %}, {% endif %}{% endfor %}
**期刊:** {{publicationTitle}} {{university}}
**类别:** {{itemType}} {{thesisType}}
**Level:** {% if archive %}{{archive}}{% endif %} {% if archiveLocation%}{{archiveLocation}}{% endif %}

>- **Url**: [Open online]({{url}})
>- **zotero entry**: {{pdfZoteroLink}}
>- **open pdf**: [zotero]({{select}})
---

# Abstract:
{{abstractNote}}


# 概要


# 方法




## Imported: {{importDate | format("YYYY-MM-DD h:mm a")}}


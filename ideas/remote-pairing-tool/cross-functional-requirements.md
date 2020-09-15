* Usability

The tool should be easily usable. One shouldn't need a user manual to use it.
It should also be quick in terms of visual feedback when doing actions.

* Accessibility

People with disabilities should NOT be annoyed when using the tool. We have to
consider what kind of accessibility features we can bake into the product for
making it easy for all of our users to use the product, no matter their health.
Some thoughts - how people with disability in the eye will easily use the tool?
for example, people who have some sort of blindness. 

* Performance

The tool has to be performant in the sense that
- It has to be smooth in ideal situations (good network)
- It has to use the least amount of resources to be performant

* Internationilization

Not everyone knows or understands English, and they shouldn't need to know it
or understand it. Many countries have their native language as the medium of
education and people are very comfortable and feel at ease when using their
native language. The tool should make people comfortable and not uncomfortable.
We need to be able to provide internationalization features where we can
support as many languages as possible based on our user base, and keep extending
it so that anyone in the world can use our product and are not restricted
because of it's language.

* Configurability
* Security
    * Authentication / Authorization. Confidentiality.

        Only people who are authenticated - whose identity is known to the
        system, can access the system. Every feature of the system can be
        mapped to roles and users can be assigned roles. Users with a particular
        role can then access features available to that role - Role Based Access
        Control (RBAC). So, only people with sufficient access / access level,
        can access appropriate features. 

        When the product caters to organizations, something to consider is using
        LDAP, SSO, Open ID Connect and other authentication / authorization
        systems that the organization might already have and we can just reuse
        them instead of asking users to signup in a new system.

    * Integrity

        No one can tamper any data in a malicious manner.

    * Availability

        No one can attack the system to bring it down. For example DoS - Denial
        of Service attack, DDos - Distributed Denial of Service attack.
        The system has to be up and running for our loyal users, and not be
        down because of malicious hackers.

    * Auditability

        User should be able to audit things happening in on their account.
        When the product caters to organizations, organization level auditability
        is something to consider.

    * Data Laws

    We need to obey the Data Laws in different locations. For example GDPR. So
    that users trust us and can use our product, as we are law abiding citizens
    of Earth.

* Observability

    The user should be able to observe what is going on in their system and why
    something is slow or not working when using their tool.

    The developers of the system should also be able to monitor and observe all
    the systems any time and be alerted of issues in user side (client side) or
    server side (backend)

* Extensibility

    If the users are looking for extending features of the product - consider it.
    Some sort of customization or integration with existing tools.

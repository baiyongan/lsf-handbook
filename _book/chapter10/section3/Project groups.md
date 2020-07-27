# Project groups

When you are configuring your installation of License Scheduler in project mode, you can choose to configure projects, or extend your project configuration further to form hierarchical project groups.

Project groups pool multiple service domains together and treat them as one source for licenses, and distribute them in a hierarchical fairshare tree. The leaves of the policy tree are the license projects that jobs can belong to. Each project group in the tree has a set of values, including shares and limits.

License ownership is applied at the leaf level; that is, on individual license projects. Ownership of a given internal node equals to sum of the ownership of all of its direct children.

Each feature has its own hierarchical group, but features can share hierarchy. The hierarchical scheduling is done per feature across service domains.

- projects

  Projects alone apply one distribution policy within one service domain. The same local distribution policy can be applied to more than one service domain, but is implemented locally.

- groups of projects

  Groups of projects apply one distribution policy within one service domain, but assign shares and ownership to groups of projects for greater flexibility. With group license ownership, projects trigger preemption either when the project is using fewer licenses than it owns or when the group to which the project belongs is using fewer licenses than the group owns.

- project groups

  Projects groups apply one distribution policy across multiple service domains following the configured hierarchical structure. You can also use project groups to apply hard limits to the number of licenses that are distributed to each project.After configuration, the same project group hierarchy can be used for more than one feature.

## When to use groups of projects

Grouping projects together in project mode is most appropriate for your needs if:

- Licenses are owned at multiple levels, for example by a department and also by projects within the department.
- License ownership is within one service domain. As for ungrouped projects, distribution policies are implemented locally for groups of projects.

## When to use project groups

Extending your configuration to include project groups is most appropriate for your needs if:

- License ownership spans service domains.
- One distribution policy must be applied across several service domains.
- Project limits must be applied across clusters.

**Note**If required, use LSF to configure license project limits within one cluster.
---
title: "Adding self registering keys to lua-factory"
excerpt: "14th May - 3rd June"
header: 
  teaser: "/assets/gnome.png"

tags:
  - GNOME
  - GSoC
  - GNOME Games
  - Grilo
---

For the past few weeks I've been hacking away at GNOME Games and Grilo. Here's what I've done so far.

## May 14th - June 3rd

My first task was to fetch metadata using `thegamesdb` and use it to get developer and publisher of a game to GNOME Games. For this, I had to add the appropriate system keys to Grilo, the only problem being the keys in question were too app-specific to be added as system keys and there was no provision of self registering keys in lua based sources.

### The struggle

The solution was pretty simple, I began implementing self registering keys to Grilo for lua sources to use all the while fixing any bugs I encountered on the way. 

Bastien Nocera, gave me a very bright idea to register new keys while setting their value to GRL_DATA itself. I completed this by implementing two function in Grilo.
  * grl_data_set_for_id ()
  * grl_data_add_for_id ()

### How do they work?

```c_cpp
void grl_data_set_for_id (GrlData *data, const gchar *key_name, const GValue *value);
```
The `key_name` to be registered, `value` to be set and `data` object are first passed as parameter to the function.

```c_cpp
  registry = grl_registry_get_default ();
  key_id = grl_registry_lookup_metadata_key (registry, key_name);
```
The key_name is then looked up in the registry for any matching GrlKeyID.

```c_cpp
  if (key_id != GRL_METADATA_KEY_INVALID) {
    grl_data_set (data, key_id, value);
  }
```
If found, the data is set normally using grl_data_set ().

```c_cpp
else {
    switch (G_VALUE_TYPE (value)) {
    case G_TYPE_INT:
      spec = g_param_spec_int (key_name,
                               key_name,
                               key_name,
                               0, G_MAXINT,
                               0,
                               G_PARAM_STATIC_STRINGS | G_PARAM_READWRITE);

      key_id = grl_registry_register_metadata_key (registry, spec, GRL_METADATA_KEY_INVALID, NULL);
      grl_data_set (data, key_id, value);
      break;

    case G_TYPE_INT64:
      spec = g_param_spec_int64 (key_name,
                                 key_name,
                                 key_name,
                                 -1, G_MAXINT64,
                                 -1,
                                 G_PARAM_STATIC_STRINGS | G_PARAM_READWRITE);

      key_id = grl_registry_register_metadata_key (registry, spec, GRL_METADATA_KEY_INVALID, NULL);
      grl_data_set (data, key_id, value);
      break;

    case G_TYPE_STRING:
      spec = g_param_spec_string (key_name,
                                  key_name,
                                  key_name,
                                  NULL,
                                  G_PARAM_STATIC_STRINGS | G_PARAM_READWRITE);

      key_id = grl_registry_register_metadata_key (registry, spec, GRL_METADATA_KEY_INVALID, NULL);
      grl_data_set (data, key_id, value);
      break;

    case G_TYPE_BOOLEAN:
      spec = g_param_spec_boolean (key_name,
                                   key_name,
                                   key_name,
                                   FALSE,
                                   G_PARAM_STATIC_STRINGS | G_PARAM_READWRITE);

      key_id = grl_registry_register_metadata_key (registry, spec, GRL_METADATA_KEY_INVALID, NULL);
      grl_data_set (data, key_id, value);
      break;

    case G_TYPE_FLOAT:
      spec = g_param_spec_float (key_name,
                                 key_name,
                                 key_name,
                                 0, G_MAXFLOAT,
                                 0,
                                 G_PARAM_STATIC_STRINGS | G_PARAM_READWRITE);

      key_id = grl_registry_register_metadata_key (registry, spec, GRL_METADATA_KEY_INVALID, NULL);
      grl_data_set (data, key_id, value);
      break;

    default:
      if (type == G_TYPE_DATE_TIME) {
        spec = g_param_spec_boxed (key_name,
                                   key_name,
                                   key_name,
                                   G_TYPE_DATE_TIME,
                                   G_PARAM_STATIC_STRINGS | G_PARAM_READWRITE);

        key_id = grl_registry_register_metadata_key (registry, spec, GRL_METADATA_KEY_INVALID, NULL);
        grl_data_set (data, key_id, value);
      }
    }
  }
}
```
If not found, the appropriate g_param_spec is defined for that particular `G_TYPE`, the key is then registered using grl_registry_regsiter_metadata_key () and value is set using grl_data_set (). This function sets the first value associated with `key_name` in `data`. If `key_name` already has a first `value`, old value is replaced by the new one.


```c_cpp
void grl_data_set_for_id (GrlData *data, const gchar *key_name, const GValue *value);
```
This function also works similarly to the same as above one, with only a few minor differences.
The value associated with `key_name` to `data` is appended instead of set. This `key_name` is used to create a new `GParamSpec` instance, which is further used to create and register a key using grl_registry_register_metadata_key(). The value is added using grl_data_add* instead of grl_data_set ().

After implementing these, I was just a step away from allowing lua sources to have self registering keys. The only work left was to modify lua plugins to use the above functions when metadata is added to `GrlMedia`.

Now, adding self registering keys was as easy as typing

```lua
    if game.Developer then
      media.developer = game.Developer.xml
    end
```
Lastly, I added a test case to grilo-plugins to verify these changes. With this, allowing self registering keys to Grilo was over.

### Adding Developer & Publisher to Games

GNOME Games currently has a very basic UI. I added Developer & Publisher to Game object which will further be used for segregating games into different `views`, such as a `Developer view` allowing users to select games from a particular developer and similarly a `Publisher view`. I've already started working on this and will be posting more on this soon.

I hope to see you all at GUADEC this year.
Cheers!







